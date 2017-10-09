---
title: "problemas de ligação de aaaTroubleshoot Azure ponto a site | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de ligação de ponto a site."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Resolução de problemas: Problemas de ligação de ponto a site do Azure

Este artigo apresenta uma lista de problemas de ligação de ponto a site comuns que podem ocorrer. Também descreve possíveis causas e soluções para esses problemas.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Erro de cliente VPN: não foi possível encontrar um certificado

### <a name="symptom"></a>Sintoma

Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:

**Não foi possível encontrar um certificado que pode ser utilizado com este protocolo de autenticação extensível. (Erro 798)**

### <a name="cause"></a>Causa

Este problema ocorre se o certificado de cliente Olá Faltam **certificados - User\Personal\Certificates atual**.

### <a name="solution"></a>Solução

Certifique-se de que certificado de cliente Olá está instalado no Olá seguinte localização do arquivo de certificados de Olá (Certmgr.msc):
 
**Certificados - User\Personal\Certificates atual**

Para obter mais informações sobre como tooinstall Olá certificado de cliente, consulte [gerar e exportar certificados para ligações ponto a site](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Ao importar o certificado de cliente Olá, não selecione Olá **ativar a proteção forte por chave privada** opção.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Erro de cliente VPN: mensagem de saudação recebida era inesperada ou formatado incorretamente

### <a name="symptom"></a>Sintoma

Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:

**foi recebida uma mensagem Olá era inesperada ou incorretamente formatado. (Erro 0x80090326)**

### <a name="cause"></a>Causa

Este problema ocorre se a chave pública do certificado de raiz Olá não é carregado para o gateway de VPN do Azure Olá. Também pode ocorrer se a chave de Olá está danificada ou expirada.

### <a name="solution"></a>Solução

tooresolve este problema, verifique o estado de Olá de raiz de Olá de certificado no Olá toosee portal do Azure se foi revogado. Se não for revogado, experimente o certificado de raiz de Olá toodelete e reupload. Para obter mais informações, consulte [criar certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Erro de cliente VPN: uma cadeia de certificados processada, mas foi terminado 

### <a name="symptom"></a>Sintoma 

Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:

**Uma cadeia de certificados processados mas terminada num certificado de raiz que não é considerado fidedigno pelo fornecedor de confiança Olá.**

### <a name="solution"></a>Solução

1. Certifique-se de que Olá seguintes certificados na localização correta Olá:

    | Certificado | Localização |
    | ------------- | ------------- |
    | AzureClient.pfx  | User\Personal\Certificates atual |
    | Azuregateway -*GUID*. cloudapp.net  | Autoridades de certificação de raiz User\Trusted atual|
    | AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer    | Autoridades de certificação de raiz local Computer\Trusted|

2. Se os certificados de Olá já estão na localização de Olá, tente certificados de Olá toodelete e reinstalá-los. Olá  **azuregateway -*GUID*. cloudapp.net** certificado está no pacote configuração de cliente VPN de Olá que transferiu a partir do Olá portal do Azure. Pode utilizar o ficheiro archivers tooextract Olá os ficheiros do pacote de Olá.

## <a name="file-download-error-target-uri-is-not-specified"></a>Erro de transferência de ficheiro: o URI de destino não for especificado.

### <a name="symptom"></a>Sintoma

Receber Olá seguir a mensagem de erro:

**Erro de transferência do ficheiro. URI de destino não está especificado.**

### <a name="cause"></a>Causa 

Este problema ocorre devido a um tipo de gateway incorreto. 

### <a name="solution"></a>Solução

Olá, tipo de gateway VPN tem de ser **VPN**, e Olá tipo de VPN tem de ser **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Erro de cliente VPN: falha no script personalizado VPN do Azure 

### <a name="symptom"></a>Sintoma

Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:

**Script personalizado (tooupdate o encaminhamento de tabela) falha. (Erro 8007026f)**

### <a name="cause"></a>Causa

Este problema pode ocorrer se estiver a tentar ligação de VPN do tooopen Olá ponto a site utilizando um atalho.

### <a name="solution"></a>Solução 

Abra o pacote de VPN Olá diretamente em vez de abri-lo a partir do atalho Olá.

## <a name="cannot-install-hello-vpn-client"></a>Não é possível instalar o cliente VPN Olá

### <a name="cause"></a>Causa 

Um certificado adicional é gateway de VPN de Olá tootrust necessária para a rede virtual. certificado de Olá está incluído no pacote configuração de cliente VPN de Olá que é gerado a partir de Olá portal do Azure.

### <a name="solution"></a>Solução

Extraia o pacote de configuração de cliente VPN Olá e localizar o ficheiro. cer de Olá. Olá tooinstall de certificado, siga estes passos:

1. Abra mmc.exe.
2. Adicionar Olá **certificados** snap-in.
3. Selecione Olá **computador** conta do computador local Olá.
4. Contexto Olá **autoridades de certificação de raiz fidedigna** nós. Clique em **todas as tarefas** > **importação**e o ficheiro. cer toohello de procurar extraiu de pacote de configuração de cliente VPN Olá.
5. Reinicie o computador de Olá. 
6. Tente cliente VPN de Olá tooinstall.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Erro de portal do Azure: Falha ao gateway de VPN do toosave Olá, e os dados de Olá inválidos

### <a name="symptom"></a>Sintoma

Quando tenta alterações de Olá toosave para gateway de VPN Olá no Olá portal do Azure, receber Olá seguir a mensagem de erro:

**Gateway de rede virtual falha toosave &lt;* nome do gateway*&gt;. Dados do certificado &lt; *ID de certificado* &gt; é invalid.* *

### <a name="cause"></a>Causa 

Este problema pode ocorrer se Olá raiz certificado chave pública que carregou contém um caráter inválido, por exemplo, um espaço.

### <a name="solution"></a>Solução

Certifique-se de que os dados de Olá no certificado de Olá não contém carateres inválidos, tais como as quebras de linha (mudanças). valor inteiro Olá deve ser uma linha de tempo. Olá seguir o texto é uma amostra de certificado Olá:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Erro de portal do Azure: Falha ao gateway de VPN de Olá toosave e Olá o nome do recurso é inválido

### <a name="symptom"></a>Sintoma

Quando tenta alterações de Olá toosave para gateway de VPN Olá no Olá portal do Azure, receber Olá seguir a mensagem de erro: 

**Gateway de rede virtual falha toosave &lt;* nome do gateway*&gt;. Nome do recurso &lt; *nome do certificado tente tooupload* &gt; é inválido. o * *.

### <a name="cause"></a>Causa

Este problema ocorre porque o nome de Olá do certificado de Olá contém um caráter inválido, tais como um espaço. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Erro de portal do Azure: erro de transferência de ficheiro de pacote VPN 503

### <a name="symptom"></a>Sintoma

Quando tenta pacote de configuração do cliente VPN do toodownload Olá, receberá Olá seguir a mensagem de erro:

**Falha ao ficheiro de Olá toodownload. Detalhes do erro: erro 503. servidor de Olá está ocupado.**
 
### <a name="solution"></a>Solução

Este erro pode ser causado por um problema temporário de rede. Repita o pacote de VPN de Olá toodownload depois de alguns minutos.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>A atualização de Gateway de VPN do Azure: P2S todos os clientes são tooconnect não é possível

### <a name="cause"></a>Causa

Se o certificado de Olá é mais de 50 por cento através da respetiva duração, certificado Olá é distribuído.

### <a name="solution"></a>Solução

tooresolve este problema, crie e redistribuir novos certificados toohello os clientes VPN. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Demasiados clientes VPN ligados em simultâneo

Para cada gateway de VPN, Olá o número máximo de ligações permitidos é 128. Pode ver o número total de Olá de clientes ligados no Olá portal do Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>VPN ponto a site incorretamente adiciona uma rota 10.0.0.0/8 toohello tabela de rotas

### <a name="symptom"></a>Sintoma

Ao marcar Olá ligação VPN no cliente de ponto a site Olá, o cliente VPN Olá deve adicionar uma rota para Olá rede virtual do Azure. serviço de programa auxiliar IP Olá deve adicionar uma rota de sub-rede de Olá de clientes VPN de Olá. 

Olá intervalo de cliente VPN pertence tooa sub-rede mais pequeno de 10.0.0.0/8, tais como 10.0.12.0/24. Em vez de uma rota para 10.0.12.0/24, uma rota para 10.0.0.0/8 é adicionada que tenha a prioridade mais alta. 

Esta rota incorreta de quebras de conectividade com outras redes de no local que têm de pertencer tooanother sub-rede dentro do intervalo de 10.0.0.0/8 Olá, tais como 10.50.0.0/24, que não tenham uma rota específica definida. 

### <a name="cause"></a>Causa

Este comportamento é por predefinição para clientes Windows. Quando o cliente de Olá utiliza o protocolo PPP IPCP de Olá, obtém o endereço IP Olá para a interface de túnel hello do servidor de Olá (gateway VPN Olá neste caso). No entanto, devido a uma limitação no protocolo Olá, o cliente Olá tem máscara de sub-rede Olá. Porque não há nenhum tooget de forma, o cliente de Olá tentará máscara de sub-rede tooguess Olá com base na classe de Olá do endereço IP de interface de túnel Olá. 

Por conseguinte, uma rota foi adicionada com base no Olá mapeamento estático os seguintes: 

Se o endereço pertence tooclass A--> aplicar /8

Se o endereço pertence tooclass B--> aplicar /16

Se o endereço pertence tooclass C--> aplicar /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>Cliente VPN não é possível aceder a partilhas de ficheiros de rede

### <a name="symptom"></a>Sintoma

cliente VPN Olá estabeleceu ligação toohello rede virtual do Azure. No entanto, o cliente Olá não é possível aceder às partilhas de rede.

### <a name="cause"></a>Causa

Olá protocolo SMB é utilizado para acesso de partilha de ficheiros. Quando é iniciada a ligação de Olá, cliente VPN Olá adiciona as credenciais de sessão Olá e Olá a falha ocorre. Uma vez estabelecido ligação Olá, o cliente Olá é forçado toouse Olá cache as credenciais a autenticação Kerberos. Este processo inicia consultas toohello Centro de distribuição de chaves (um controlador de domínio) tooget um token. Porque Olá cliente liga-se de Olá Internet, poderá não ser capaz de tooreach controlador de domínio de Olá. Por conseguinte, cliente Olá não é possível efetuar a ativação pós-falha do tooNTLM de Kerberos. 

Olá apenas tempo que o cliente Olá é pedido uma credencial é quando tem um certificado válido (com SAN = UPN) emitido por Olá toowhich de domínio está associado. cliente de Olá também tem de ser fisicamente ligada toohello rede de domínio. Neste caso, o cliente de Olá tenta certificado de Olá toouse e acede toohello controlador de domínio. Em seguida, Olá Centro de distribuição de chaves devolve um erro de "KDC_ERR_C_PRINCIPAL_UNKNOWN". cliente de Olá é forçada toofail tooNTLM. 

### <a name="solution"></a>Solução

toowork em torno do problema Olá, desativar Olá colocação em cache de credenciais de domínio de Olá seguinte subchave de registo: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Não é possível localizar a ligação de VPN de ponto a site Olá no Windows após a reinstalação do cliente VPN Olá

### <a name="symptom"></a>Sintoma

Remover a ligação de VPN de ponto a site Olá e, em seguida, reinstalar o cliente VPN Olá. Nesta situação, Olá ligação VPN não está configurado com êxito. Não vir a ligação de VPN de Olá na Olá **ligações de rede** definições do Windows.

### <a name="solution"></a>Solução

problema de Olá tooresolve, eliminar Olá antigos VPN cliente ficheiros de configuração da **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, e, em seguida, execute novamente o programa de instalação de cliente VPN de Olá.
