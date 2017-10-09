---
title: "configuração de segurança de intercalação aaaSplit | Microsoft Docs"
description: "Configurar x409 certificados de encriptação"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Configuração de segurança de divisão de intercalação
serviço de divisão/intercalação do toouse Olá, deve configurar corretamente segurança. serviço de Olá faz parte da funcionalidade do dimensionamento elástico Olá da base de dados do Microsoft Azure SQL. Para obter mais informações, consulte [divisão de dimensionamento elástico e o Tutorial do serviço de intercalação](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Configurar certificados
Certificados são configurados de duas formas. 

1. [Olá tooConfigure certificado SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure certificados de cliente](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain certificados
Certificados podem ser obtidos a partir de autoridades de certificação (AC) pública ou de Olá [serviço de certificados do Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Estes são Olá preferido métodos tooobtain certificados.

Se essas opções não estiverem disponíveis, pode gerar **certificados autoassinados**.

## <a name="tools-toogenerate-certificates"></a>Certificados de toogenerate de ferramentas
* [MakeCert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>ferramentas de Olá toorun
* De um programador linha de comandos para estúdios Visual, consulte [linha de comandos do Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Se instalada, aceda a:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Obter Olá WDK de [Windows 8.1: Transferir kits e ferramentas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certificado SSL de Olá tooconfigure
Um certificado SSL é necessário tooencrypt Olá comunicação e autenticar Olá servidor. Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:

### <a name="create-a-new-self-signed-certificate"></a>Criar um novo certificado autoassinado
1. [Criar um certificado Autoassinado](#create-a-self-signed-certificate)
2. [Criar o ficheiro PFX de certificado de SSL autoassinado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
4. [Atualizar o certificado SSL no ficheiro de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)
5. [Importar a autoridade de certificação de SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>arquivo de um certificado existente de certificado Olá toouse
1. [Exportar o certificado SSL do arquivo de certificados](#export-ssl-certificate-from-certificate-store)
2. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
3. [Atualizar o certificado SSL no ficheiro de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse um certificado existente num ficheiro PFX
1. [Carregar o certificado SSL tooCloud serviço](#upload-ssl-certificate-to-cloud-service)
2. [Atualizar o certificado SSL no ficheiro de configuração de serviço](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certificados de cliente tooconfigure
Certificados de cliente são necessários na ordem tooauthenticate pedidos toohello serviço. Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:

### <a name="turn-off-client-certificates"></a>Desativar a certificados de cliente
1. [Desativar a autenticação baseada em certificados de cliente](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Emitir novos certificados de cliente autoassinado
1. [Criar uma autoridade de certificação Autoassinado](#create-a-self-signed-certification-authority)
2. [Carregar o certificado de AC tooCloud serviço](#upload-ca-certificate-to-cloud-service)
3. [Atualizar o certificado de AC no ficheiro de configuração de serviço](#update-ca-certificate-in-service-configuration-file)
4. [Emitir certificados de cliente](#issue-client-certificates)
5. [Criar ficheiros PFX para certificados de cliente](#create-pfx-files-for-client-certificates)
6. [Importar o certificado de cliente](#Import-Client-Certificate)
7. [Copie os Thumbprints de certificado de cliente](#copy-client-certificate-thumbprints)
8. [Configurar clientes permitido no Olá ficheiro de configuração de serviço](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Utilizar certificados de cliente existente
1. [Localizar a chave pública de AC](#find-ca-public-key)
2. [Carregar o certificado de AC tooCloud serviço](#Upload-CA-certificate-to-cloud-service)
3. [Atualizar o certificado de AC no ficheiro de configuração de serviço](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Copie os Thumbprints de certificado de cliente](#Copy-Client-Certificate-Thumbprints)
5. [Configurar clientes permitido no Olá ficheiro de configuração de serviço](#configure-allowed-clients-in-the-service-configuration-file)
6. [Configurar a verificação de revogação de certificado de cliente](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Pontos finais de serviço do acesso toohello podem ser restringida toospecific intervalos de endereços IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>encriptação de tooconfigure para arquivo Olá
É de um certificado de credenciais de Olá tooencrypt necessárias que são armazenadas no arquivo de metadados de Olá. Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:

### <a name="use-a-new-self-signed-certificate"></a>Utilizar um novo certificado autoassinado
1. [Criar um certificado Autoassinado](#create-a-self-signed-certificate)
2. [Criar o ficheiro PFX de certificado de encriptação autoassinado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Carregar o certificado de encriptação tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
4. [Atualizar o certificado de encriptação no ficheiro de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Utilizar um certificado existente Olá do arquivo de certificados
1. [Exportar o certificado de encriptação do arquivo de certificados](#export-encryption-certificate-from-certificate-store)
2. [Carregar o certificado de encriptação tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
3. [Atualizar o certificado de encriptação no ficheiro de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Utilizar um certificado existente num ficheiro PFX
1. [Carregar o certificado de encriptação tooCloud serviço](#upload-encryption-certificate-to-cloud-service)
2. [Atualizar o certificado de encriptação no ficheiro de configuração de serviço](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>configuração predefinida de Olá
configuração predefinida de Olá nega todos os acesso toohello ponto final de HTTP. Este é Olá recomendado definição, uma vez que os pontos finais do Olá pedidos toothese podem transportar as informações confidenciais, como as credenciais da base de dados.
configuração predefinida de Olá permite que todos os acesso toohello ponto final de HTTPS. Esta definição pode ser restringida adicional.

### <a name="changing-hello-configuration"></a>Alterar Olá configuração
Olá grupo de regras de controlo de acesso que se aplicam tooand endpoint estão configuradas no Olá  **<EndpointAcls>**  secção Olá **ficheiro de configuração do serviço**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

regras de Olá num grupo de controlo de acesso estão configuradas num <AccessControl name=""> secção do ficheiro de configuração do serviço de Olá. 

formato de Olá é explicado na documentação de listas de controlo de acesso de rede.
Por exemplo, tooallow IPs apenas na Olá intervalo 100.100.0.0 too100.100.255.255 tooaccess Olá ponto final de HTTPS, regras de Olá deverá ter o seguinte aspeto:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Negação de prevenção de serviço
Existem dois mecanismos diferentes suportado toodetect e impedem ataques Denial of Service:

* Restringir o número de pedidos em simultâneo por anfitrião remoto (desativado por predefinição)
* Restringir a taxa de acesso por anfitrião remoto (por predefinição)

Estas baseiam-se nas funcionalidades Olá mais documentadas em segurança IP dinâmica no IIS. Quando alterar esta configuração cuidado com de Olá seguintes fatores:

* comportamento de Olá de proxies e os dispositivos de tradução de endereços de rede através de informações do anfitrião remoto de Olá
* Cada recurso de tooany pedido na função da web Olá é considerado (por exemplo, carregar scripts, imagens, etc.)

## <a name="restricting-number-of-concurrent-accesses"></a>Restringir o número de acessos simultâneos
definições de Olá que configurar este comportamento são:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Altere DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable esta proteção.

## <a name="restricting-rate-of-access"></a>Restringir a taxa de acesso
definições de Olá que configurar este comportamento são:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Configurar Olá resposta tooa negou o pedido
Olá seguinte definição configura Olá resposta tooa negada o pedido:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Consulte a documentação do toohello para segurança IP dinâmica no IIS para outros valores suportados.

## <a name="operations-for-configuring-service-certificates"></a>Operações para configurar certificados de serviço
Este tópico é apenas de referência. Siga os passos de configuração de Olá descritos em:

* Configurar um certificado SSL Olá
* Configurar certificados de cliente

## <a name="create-a-self-signed-certificate"></a>Criar um certificado autoassinado
Execute:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n com Olá URL de serviço. Carateres universais ("CN = * .cloudapp .net") e os nomes alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") são suportados.
* -i com data de expiração do certificado Olá criar uma palavra-passe segura e especifique-quando lhe for pedido.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Criar o ficheiro PFX de certificado SSL autoassinado
Execute:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades expandidas

## <a name="export-ssl-certificate-from-certificate-store"></a>Exportar o certificado SSL do arquivo de certificados
* Localizar o certificado
* Clique em ações -> todas as tarefas -> Exportar...
* Exportar o certificado para um. Ficheiro PFX com estas opções:
  * Sim, exportar a chave privada Olá
  * Incluir todos os certificados no caminho de certificação de Olá se for possível * exportar propriedades expandidas tudo

## <a name="upload-ssl-certificate-toocloud-service"></a>Carregar o serviço de toocloud do certificado SSL
Carregue o certificado com Olá existente ou gerado. Ficheiro PFX com Olá par de chaves de SSL:

* Introduza a palavra-passe Olá a proteger as informações de chave privada Olá

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Atualizar o certificado SSL no ficheiro de configuração de serviço
Atualize o valor do thumbprint de Olá de Olá definição no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Importar a autoridade de certificação de SSL
Siga estes passos em todos os conta/máquina que irão comunicar com o serviço de Olá:

* Faça duplo clique Olá. Ficheiro CER no Explorador do Windows
* Na caixa de diálogo de certificado Olá, clique em instalar certificado...
* Importar o certificado para Olá que arquivo de autoridades de certificação de raiz fidedigna

## <a name="turn-off-client-certificate-based-authentication"></a>Desativar a autenticação baseada em certificados de cliente
Apenas a autenticação de baseada em certificado cliente é suportada e a sua desativação permitirá para acesso público toohello pontos finais do serviço, a menos que outros mecanismos estão no local (por exemplo, Microsoft Azure Virtual Network).

Altere toofalse estas definições na funcionalidade do Olá serviço de configuração ficheiro tooturn Olá:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Em seguida, copie Olá mesmo thumbprint como Olá SSL de certificado na definição de certificado Olá AC:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Criar uma autoridade de certificação autoassinado
Execute os seguintes passos toocreate tooact um certificado autoassinado como uma autoridade de certificação de Olá:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize-la

* -i com data de expiração de certificação Olá

## <a name="find-ca-public-key"></a>Localizar a chave pública de AC
Todos os certificados de cliente tem de ter foi emitidos por uma autoridade de certificação fidedigna pelo serviço de Olá. Localize toohello de chave pública de Olá autoridade de certificação que emitiu os certificados de cliente Olá que vão toobe utilizado para autenticação no tooupload ordem-toohello o serviço em nuvem.

Se o ficheiro de Olá com a chave pública Olá não estiver disponível, exportá-lo a partir do arquivo de certificados de Olá:

* Localizar o certificado
  * Olá, procure um certificado de cliente emitido pela mesma autoridade de certificação
* Faça duplo clique em certificado Olá.
* Selecione o separador de caminho de certificação de Olá na caixa de diálogo do Olá certificado.
* Faça duplo clique entrada de AC Olá no caminho de Olá.
* Toma nota de propriedades do certificado Olá.
* Fechar Olá **certificado** caixa de diálogo.
* Localizar o certificado
  * Procure Olá AC referido acima.
* Clique em ações -> todas as tarefas -> Exportar...
* Exportar o certificado para um. CER com estas opções:
  * **Não, não exportar chave privada Olá**
  * Inclua todos os certificados no caminho de certificação de Olá se possível.
  * Exporte todas as propriedades expandidas.

## <a name="upload-ca-certificate-toocloud-service"></a>Carregar o serviço de toocloud de certificado de AC
Carregue o certificado com Olá existente ou gerado. Ficheiro CER com a chave pública Olá AC.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Certificado da AC de atualização no ficheiro de configuração de serviço
Atualize o valor do thumbprint de Olá de Olá definição no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Atualizar o valor Olá Olá seguinte definição com Olá mesmo thumbprint:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Emitir certificados de cliente
Cada serviço de Olá individuais tooaccess autorizados deve ter um certificado de cliente emitido para his/hers exclusivo utilizar e deve escolher que HIS/hers proprietário tooprotect de palavra-passe segura respetiva chave privada. 

Olá, seguindo os passos tem de ser executado na mesma máquina onde Olá AC um certificado autoassinado foi gerada e armazenada de Olá:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Personalizar:

* -n com um ID de cliente de toohello que será autenticada com este certificado
* -i com data de expiração do certificado Olá
* MyID.pvk e MyID.cer com os nomes de ficheiro exclusivo para este certificado de cliente

Este comando irá solicitar uma toobe de palavra-passe criada e, em seguida, utilizado uma vez. Utilize uma palavra-passe segura.

## <a name="create-pfx-files-for-client-certificates"></a>Criar ficheiros PFX para o cliente certificados
Para cada certificado de cliente gerado, execute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizar:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades expandidas
* Olá toowhom individuais, que este certificado emitido deve escolher a palavra-passe de exportação de Olá

## <a name="import-client-certificate"></a>Importar o certificado de cliente
Cada indivíduo para o qual foi emitido um certificado de cliente deve importar par de chaves Olá máquinas Olá he/she utilizará toocommunicate com o serviço de Olá:

* Faça duplo clique Olá. Ficheiro PFX no Explorador do Windows
* Importar o certificado para Olá pessoal armazenar com, pelo menos, esta opção:
  * Incluir todas as propriedades expandidas marcadas

## <a name="copy-client-certificate-thumbprints"></a>Copie os thumbprints de certificado de cliente
Cada indivíduo para o qual foi emitido um certificado de cliente tem de seguir estes passos na ordem tooobtain Olá thumbprint his/hers certificado que será adicionado toohello ficheiro de configuração de serviço:

* Executar certmgr.exe
* Selecione o separador Personal Olá
* Faça duplo clique em certificado de cliente de Olá toobe utilizado para autenticação
* Olá certificado caixa de diálogo que se abre, selecione o separador de detalhes de Olá
* Certifique-se que apresenta Mostrar tudo
* Campo de Olá selecione denominado Thumbprint na lista de Olá
* Copiar Olá valor do thumbprint Olá * * eliminar carateres Unicode não visível à frente dígito primeiro Olá * * eliminar todos os espaços

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Configurar clientes permitido no ficheiro de configuração do serviço de Olá
Atualize o valor de Olá de Olá definição no ficheiro de configuração do serviço de Olá com uma lista separada por vírgulas de thumbprints Olá Olá certificados de cliente permitidas acesso toohello serviço os seguintes:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Configurar a verificação de revogação de certificado de cliente
não verifica a predefinição de Olá com Olá autoridade de certificação para o estado de revogação de certificados de cliente. verificações de tooturn no Olá, se Olá autoridade de certificação que emitiu certificados de cliente Olá suportar estas verificações, alterar Olá seguinte definição com um dos valores de Olá definidos no Olá X509RevocationMode enumeração:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Criar o ficheiro PFX para certificados de encriptação autoassinado
Para um certificado de encriptação, execute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizar:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:

* Sim, exportar a chave privada Olá
* Exportar todas as propriedades expandidas
* Precisa de palavra-passe de Olá ao carregar o serviço em nuvem do Olá certificado toohello.

## <a name="export-encryption-certificate-from-certificate-store"></a>Exportar o certificado de encriptação do arquivo de certificados
* Localizar o certificado
* Clique em ações -> todas as tarefas -> Exportar...
* Exportar o certificado para um. Ficheiro PFX com estas opções: 
  * Sim, exportar a chave privada Olá
  * Incluir todos os certificados no caminho de certificação de Olá se possível 
* Exportar todas as propriedades expandidas

## <a name="upload-encryption-certificate-toocloud-service"></a>Carregar o serviço de toocloud de certificado de encriptação
Carregue o certificado com Olá existente ou gerado. Ficheiro PFX com o par de chaves de encriptação de Olá:

* Introduza a palavra-passe Olá a proteger as informações de chave privada Olá

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Atualizar o certificado de encriptação no ficheiro de configuração de serviço
Atualize o valor do thumbprint de Olá de Olá definições no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Operações comuns do certificado
* Configurar um certificado SSL Olá
* Configurar certificados de cliente

## <a name="find-certificate"></a>Localizar o certificado
Siga estes passos.

1. Execute mmc.exe.
2. Ficheiro -> Adicionar/Remover Snap-in...
3. Selecione **certificados**.
4. Clique em **Adicionar**.
5. Escolha a localização do arquivo de certificados de Olá.
6. Clique em **Concluir**.
7. Clique em **OK**.
8. Expanda **certificados**.
9. Expanda o nó de arquivo de certificados de Olá.
10. Expanda o nó secundário do Olá certificado.
11. Selecione um certificado na lista de Olá.

## <a name="export-certificate"></a>Exportar certificado
No Olá **Assistente para exportar certificados**:

1. Clique em **Seguinte**.
2. Selecione **Sim**, em seguida, **chave privada do exportação Olá**.
3. Clique em **Seguinte**.
4. Selecione o formato de ficheiro de saída pretendidas Olá.
5. Verifique as opções de Olá assim o desejar.
6. Verifique **palavra-passe**.
7. Introduza uma palavra-passe segura e confirmá-la.
8. Clique em **Seguinte**.
9. Escreva ou procure um nome de ficheiro onde toostore Olá certificado (utilizar um. Extensão PFX).
10. Clique em **Seguinte**.
11. Clique em **Concluir**.
12. Clique em **OK**.

## <a name="import-certificate"></a>Importar certificado
No Assistente para importar certificados Olá:

1. Selecione a localização do arquivo de Olá.
   
   * Selecione **utilizador atual** se apenas a processos em execução em utilizador atual serão aceder ao serviço de Olá
   * Selecione **máquina Local** se outros processos neste computador forem aceder ao serviço de Olá
2. Clique em **Seguinte**.
3. Se importar de um ficheiro, confirme o caminho do ficheiro Olá.
4. Se importar um. Ficheiro PFX:
   1. Introduza a palavra-passe Olá a proteger a chave privada Olá
   2. Selecione as opções de importação
5. Selecionar certificados de "Local" em Olá seguir arquivo
6. Clique em **Browse** (Procurar).
7. Selecione arquivo de Olá pretendido.
8. Clique em **Concluir**.
   
   * Se for escolhido o arquivo de autoridade de certificação de raiz fidedigna Olá, clique em **Sim**.
9. Clique em **OK** em todas as janelas de caixa de diálogo.

## <a name="upload-certificate"></a>Carregar certificado
No Olá [Portal do Azure](https://portal.azure.com/)

1. Selecione **serviços em nuvem**.
2. Selecione o serviço em nuvem Olá.
3. No menu superior Olá, clique em **certificados**.
4. Na barra inferior de Olá, clique em **carregar**.
5. Selecione o ficheiro de certificado Olá.
6. Se é um. PFX ficheiro, introduza a palavra-passe de Olá para a chave privada Olá.
7. Depois de concluída, copie o thumbprint do certificado Olá da nova entrada de Olá na lista de Olá.

## <a name="other-security-considerations"></a>Outras considerações de segurança
as definições de SSL de Olá descritas neste documento encriptam a comunicação entre o serviço de Olá e respetivos clientes quando o ponto final de HTTPS de Olá é utilizado. Isto é importante porque as credenciais de acesso de base de dados e possivelmente outras informações confidenciais contidas na comunicação de Olá. Tenha em atenção, no entanto, de que o serviço de Olá persistir estado interno, incluindo credenciais, no respetivas internas tabelas na base de dados do Microsoft Azure SQL Olá que forneceu para o armazenamento de metadados na sua subscrição do Microsoft Azure. A base de dados foi definido como parte da Olá seguinte definição no ficheiro de configuração de serviço (. Ficheiro CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

As credenciais armazenadas nesta base de dados são encriptadas. No entanto, como melhor prática, certifique-se de que são mantidas funções web e de trabalho das implementações serviço cópia de segurança toodate e segura à medida que têm acesso toohello metadados da base de dados e Olá certificado utilizado para encriptação e desencriptação de credenciais armazenadas. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

