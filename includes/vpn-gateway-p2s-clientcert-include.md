Cada computador cliente que liga tooa a VNet com ponto a Site tem de ter um certificado de cliente instalado. certificado de cliente Olá é gerado a partir do certificado de raiz de Olá e instalado em cada computador cliente. Se não está instalado um certificado de cliente válido e o cliente de Olá tenta tooconnect toohello VNet, a autenticação falha.

Ou pode gerar um certificado exclusivo para cada cliente, ou pode utilizar Olá mesmo certificado para vários clientes. certificados de cliente exclusivos Olá partido toogenerating é Olá capacidade toorevoke um certificado único. Caso contrário, se vários clientes forem utilizar Olá mesmo certificado de cliente e terá de toorevoke, ter toogenerate e instalar novos certificados para Olá todos os clientes que utilizam esse tooauthenticate de certificado.

Pode gerar os certificados de cliente utilizando Olá seguintes métodos:

- **Certificado da empresa:**

  - Se estiver a utilizar uma solução de certificados de empresa, gerar um certificado de cliente com o formato de valor de nome comum Olá 'name@yourdomain.com', em vez de Olá ' domínio ' /formato.
  - Certifique-se de que o certificado de cliente Olá é baseado no modelo de certificado de 'User' Olá com autenticação de cliente como Olá primeiro item de lista de utilização de Olá, em vez de Smart Card início de sessão, etc. Pode verificar o certificado de Olá, fazendo duplo clique em certificado de cliente Olá e visualize **detalhes > utilização de chave avançada**.

- **Certificado de raiz autoassinado:** é importante que segue Olá passos dos artigos de certificado Olá P2S abaixo. Caso contrário, os certificados de cliente Olá que criar não ser compatíveis com ligações P2S e os clientes recebem um erro quando tenta tooconnect. passos de Olá dos seguintes artigos de Olá geram um certificado de cliente compatível: 

  * [Instruções do Windows 10 PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): estas instruções necessitam de certificados de toogenerate do Windows 10 e o PowerShell. certificados de Olá que são gerados podem ser instalados em qualquer cliente P2S suportada.
  * [Instruções de MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): Utilize MakeCert se não tiver acesso tooa Windows 10 computador toouse toogenerate certificados. MakeCert preterido, mas pode continuar a utilizar o MakeCert toogenerate certificados. certificados de Olá que são gerados podem ser instalados em qualquer cliente P2S suportada.

  Ao gerar um certificado de cliente a partir de um certificado de raiz autoassinado utilizando Olá precedente instruções, tiver automaticamente instalado no computador de Olá que utilizou toogenerate-lo. Se quiser tooinstall um certificado de cliente no outro computador cliente, terá de tooexport-o como um ficheiro. pfx, juntamente com a cadeia de certificados inteira Olá. Esta ação cria um ficheiro. pfx que contém informações de certificado de raiz Olá que é necessárias para autenticar Olá toosuccessfully de cliente. Para os passos tooexport um certificado, consulte [certificados - exportar um certificado de cliente](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
