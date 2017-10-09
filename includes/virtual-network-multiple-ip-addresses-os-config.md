## <a name="os-config"></a>Adicionar endereços IP tooa sistema de operativo VM

Ligue e início de sessão tooa VM que criou com vários endereços IP privados. Tem de adicionar manualmente todos os Olá endereços IP privados (incluindo Olá primário) que adicionou toohello VM. Conclua os seguintes passos para o seu sistema de operativo VM de Olá:

### <a name="windows"></a>Windows

1. A partir de uma linha de comandos, escreva *ipconfig /all*.  Vê apenas Olá *primário* endereço IP privado (através de DHCP).
2. Tipo *ncpa.cpl* no Olá de tooopen de linha de comandos Olá **ligações de rede** janela.
3. Abrir propriedades Olá adaptador adequado Olá: **ligação de área Local**.
4. Faça duplo clique em protocolo IP versão 4 (IPv4).
5. Selecione **Olá utilize os seguintes endereços IP** e introduza Olá os seguintes valores:

    * **Endereço IP**: introduza Olá *primário* endereço IP privado
    * **Máscara de sub-rede**: Conjunto baseado na sua sub-rede. Por exemplo, se hello sub-rede é um /24 sub-rede e sub-rede Olá máscara é 255.255.255.0.
    * **Gateway predefinido**: Olá primeiro endereço IP da sub-rede Olá. Se a sub-rede 10.0.0.0/24, endereço IP do gateway Olá for de 10.0.0.1.
    * Clique em **Olá utilize os seguintes endereços de servidor DNS** e introduza Olá os seguintes valores:
        * **Servidor DNS preferencial**: Se não estiver a utilizar o seu próprio servidor DNS, introduza 168.63.129.16.  Se estiver a utilizar o seu próprio servidor DNS, introduza o endereço IP Olá para o servidor.
    * Clique em Olá **avançadas** botão e adicionar endereços IP adicionais. Adicione cada Olá secundários endereços IP privados listados no passo 8 toohello NIC com Olá mesma sub-rede especificada para o endereço IP primário Olá.
        >[!WARNING] 
        >Se não siga os passos de Olá acima corretamente, poderá perder conectividade tooyour VM. Certifique-se de que as informações de Olá introduzidas para o passo 5 são precisos antes de continuar.

    * Clique em **OK** tooclose saída definições Olá TCP/IP e, em seguida, **OK** novamente tooclose Olá as definições da placa. A ligação RDP é restabelecida.

6. A partir de uma linha de comandos, escreva *ipconfig /all*. Todos os endereços IP adicionados por si são apresentados e o DHCP é desativado.


### <a name="validation-windows"></a>Validação (Windows)

tooensure toohello tooconnect capaz de internet da sua configuração de IP secundária através de Olá que IP público associados, depois de adicioná-la corretamente utilizando os passos acima, utilize Olá os seguintes comandos:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para configurações de IP secundárias, só pode ping toohello Internet se a configuração de Olá tem um endereço IP público com associados. Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Abra uma janela de terminal.
2. Certifique-se que utilizador do Olá raiz. Se não estiver, introduza Olá os seguintes comandos:

    ```bash
    sudo -i
    ```

3. Atualize o ficheiro de configuração de Olá Olá da interface de rede (assumindo que 'eth0').

    * Manter Olá item de linha existente do dhcp. endereço IP primário Olá permanece configurado que estava anteriormente.
    * Adicione uma configuração para um endereço IP estático adicional com Olá os seguintes comandos:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Deverá ver um ficheiro .cfg.
4. Ficheiro Olá aberta. Deverá ver Olá seguintes linhas no fim de Olá do ficheiro de Olá:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Adicione Olá seguintes linhas após as linhas de Olá existentes neste ficheiro:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Guarde o ficheiro de Olá utilizando Olá os seguintes comandos:

    ```bash
    :wq
    ```

7. Interface de rede de Olá repor com Olá os seguintes comandos:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Execute ifdown e ifup no Olá mesmo linha se utilizar uma ligação remota.
    >

8. Certifique-se de que o endereço IP Olá é adicionado a interface de rede toohello com Olá os seguintes comandos:

    ```bash
    ip addr list eth0
    ```

    Deverá ver que adicionou como parte da lista de Olá de endereços de IP de Olá.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS e outros)

1. Abra uma janela de terminal.
2. Certifique-se que utilizador do Olá raiz. Se não estiver, introduza Olá os seguintes comandos:

    ```bash
    sudo -i
    ```

3. Introduza a sua palavra-passe e siga as instruções, conforme solicitado. Assim que estiver utilizador de raiz de Olá, navegue toohello pasta de scripts de rede com Olá os seguintes comandos:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Olá lista relacionado com ficheiros de ifcfg utilizando Olá os seguintes comandos:

    ```bash
    ls ifcfg-*
    ```

    Deverá ver *ifcfg eth0* como um dos ficheiros de Olá.

5. tooadd um endereço IP, crie um ficheiro de configuração para o mesmo conforme mostrado abaixo. Tenha em atenção que tem de criar um ficheiro para cada configuração de IP.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Abra Olá *ifcfg-eth0:0* ficheiro com Olá os seguintes comandos:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Adicionar ficheiros de conteúdo toohello, *eth0:0* neste caso, com Olá os seguintes comandos. Informações de tooupdate se basear-se no seu endereço IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Guarde o ficheiro de Olá com Olá os seguintes comandos:

    ```bash
    :wq
    ```

9. Reinicie os serviços de rede Olá e certifique-se as alterações de Olá com êxito executando Olá os seguintes comandos:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Deverá ver que adicionou, endereços de IP de Olá *eth0:0*, na lista de Olá devolvida.

### <a name="validation-linux"></a>Validação (Linux)

tooensure são toohello tooconnect capaz de internet da sua configuração de IP secundária através de IP público Olá associados-lo, utilize Olá os seguintes comandos:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para configurações de IP secundárias, só pode ping toohello Internet se a configuração de Olá tem um endereço IP público com associados. Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello Internet.

Para VMs com Linux, quando tentar toovalidate conectividade de saída de uma NIC secundária, poderá ser necessário tooadd de rotas adequado. Existem muitas formas toodo isto. Consulte a documentação adequada para a distribuição de Linux. seguinte Olá é um método tooaccomplish:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Ser tooreplace se:
    - **10.0.0.5** com Olá privada endereço que tenha um IP público endereço IP associado tooit
    - **10.0.0.1** gateway predefinido de tooyour
    - **eth2** toohello nome do seu NIC secundário
