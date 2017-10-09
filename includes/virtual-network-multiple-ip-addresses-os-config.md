## <span data-ttu-id="2dfd4-101"><a name="os-config"></a>Adicionar endereços IP tooa sistema de operativo VM</span><span class="sxs-lookup"><span data-stu-id="2dfd4-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="2dfd4-102">Ligue e início de sessão tooa VM que criou com vários endereços IP privados.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="2dfd4-103">Tem de adicionar manualmente todos os Olá endereços IP privados (incluindo Olá primário) que adicionou toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="2dfd4-104">Conclua os seguintes passos para o seu sistema de operativo VM de Olá:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="2dfd4-105">Windows</span><span class="sxs-lookup"><span data-stu-id="2dfd4-105">Windows</span></span>

1. <span data-ttu-id="2dfd4-106">A partir de uma linha de comandos, escreva *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="2dfd4-107">Vê apenas Olá *primário* endereço IP privado (através de DHCP).</span><span class="sxs-lookup"><span data-stu-id="2dfd4-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="2dfd4-108">Tipo *ncpa.cpl* no Olá de tooopen de linha de comandos Olá **ligações de rede** janela.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="2dfd4-109">Abrir propriedades Olá adaptador adequado Olá: **ligação de área Local**.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="2dfd4-110">Faça duplo clique em protocolo IP versão 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="2dfd4-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="2dfd4-111">Selecione **Olá utilize os seguintes endereços IP** e introduza Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="2dfd4-112">**Endereço IP**: introduza Olá *primário* endereço IP privado</span><span class="sxs-lookup"><span data-stu-id="2dfd4-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="2dfd4-113">**Máscara de sub-rede**: Conjunto baseado na sua sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="2dfd4-114">Por exemplo, se hello sub-rede é um /24 sub-rede e sub-rede Olá máscara é 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="2dfd4-115">**Gateway predefinido**: Olá primeiro endereço IP da sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="2dfd4-116">Se a sub-rede 10.0.0.0/24, endereço IP do gateway Olá for de 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="2dfd4-117">Clique em **Olá utilize os seguintes endereços de servidor DNS** e introduza Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="2dfd4-118">**Servidor DNS preferencial**: Se não estiver a utilizar o seu próprio servidor DNS, introduza 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="2dfd4-119">Se estiver a utilizar o seu próprio servidor DNS, introduza o endereço IP Olá para o servidor.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="2dfd4-120">Clique em Olá **avançadas** botão e adicionar endereços IP adicionais.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="2dfd4-121">Adicione cada Olá secundários endereços IP privados listados no passo 8 toohello NIC com Olá mesma sub-rede especificada para o endereço IP primário Olá.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="2dfd4-122">Se não siga os passos de Olá acima corretamente, poderá perder conectividade tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="2dfd4-123">Certifique-se de que as informações de Olá introduzidas para o passo 5 são precisos antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="2dfd4-124">Clique em **OK** tooclose saída definições Olá TCP/IP e, em seguida, **OK** novamente tooclose Olá as definições da placa.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="2dfd4-125">A ligação RDP é restabelecida.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="2dfd4-126">A partir de uma linha de comandos, escreva *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="2dfd4-127">Todos os endereços IP adicionados por si são apresentados e o DHCP é desativado.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="2dfd4-128">Validação (Windows)</span><span class="sxs-lookup"><span data-stu-id="2dfd4-128">Validation (Windows)</span></span>

<span data-ttu-id="2dfd4-129">tooensure toohello tooconnect capaz de internet da sua configuração de IP secundária através de Olá que IP público associados, depois de adicioná-la corretamente utilizando os passos acima, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="2dfd4-130">Para configurações de IP secundárias, só pode ping toohello Internet se a configuração de Olá tem um endereço IP público com associados.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="2dfd4-131">Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2dfd4-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2dfd4-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="2dfd4-133">Abra uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-133">Open a terminal window.</span></span>
2. <span data-ttu-id="2dfd4-134">Certifique-se que utilizador do Olá raiz.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-134">Make sure you are hello root user.</span></span> <span data-ttu-id="2dfd4-135">Se não estiver, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="2dfd4-136">Atualize o ficheiro de configuração de Olá Olá da interface de rede (assumindo que 'eth0').</span><span class="sxs-lookup"><span data-stu-id="2dfd4-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="2dfd4-137">Manter Olá item de linha existente do dhcp.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="2dfd4-138">endereço IP primário Olá permanece configurado que estava anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="2dfd4-139">Adicione uma configuração para um endereço IP estático adicional com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="2dfd4-140">Deverá ver um ficheiro .cfg.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="2dfd4-141">Ficheiro Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-141">Open hello file.</span></span> <span data-ttu-id="2dfd4-142">Deverá ver Olá seguintes linhas no fim de Olá do ficheiro de Olá:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="2dfd4-143">Adicione Olá seguintes linhas após as linhas de Olá existentes neste ficheiro:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="2dfd4-144">Guarde o ficheiro de Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="2dfd4-145">Interface de rede de Olá repor com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="2dfd4-146">Execute ifdown e ifup no Olá mesmo linha se utilizar uma ligação remota.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="2dfd4-147">Certifique-se de que o endereço IP Olá é adicionado a interface de rede toohello com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="2dfd4-148">Deverá ver que adicionou como parte da lista de Olá de endereços de IP de Olá.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="2dfd4-149">Linux (Redhat, CentOS e outros)</span><span class="sxs-lookup"><span data-stu-id="2dfd4-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="2dfd4-150">Abra uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-150">Open a terminal window.</span></span>
2. <span data-ttu-id="2dfd4-151">Certifique-se que utilizador do Olá raiz.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-151">Make sure you are hello root user.</span></span> <span data-ttu-id="2dfd4-152">Se não estiver, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="2dfd4-153">Introduza a sua palavra-passe e siga as instruções, conforme solicitado.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="2dfd4-154">Assim que estiver utilizador de raiz de Olá, navegue toohello pasta de scripts de rede com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="2dfd4-155">Olá lista relacionado com ficheiros de ifcfg utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="2dfd4-156">Deverá ver *ifcfg eth0* como um dos ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="2dfd4-157">tooadd um endereço IP, crie um ficheiro de configuração para o mesmo conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="2dfd4-158">Tenha em atenção que tem de criar um ficheiro para cada configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="2dfd4-159">Abra Olá *ifcfg-eth0:0* ficheiro com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="2dfd4-160">Adicionar ficheiros de conteúdo toohello, *eth0:0* neste caso, com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="2dfd4-161">Informações de tooupdate se basear-se no seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="2dfd4-162">Guarde o ficheiro de Olá com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="2dfd4-163">Reinicie os serviços de rede Olá e certifique-se as alterações de Olá com êxito executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="2dfd4-164">Deverá ver que adicionou, endereços de IP de Olá *eth0:0*, na lista de Olá devolvida.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="2dfd4-165">Validação (Linux)</span><span class="sxs-lookup"><span data-stu-id="2dfd4-165">Validation (Linux)</span></span>

<span data-ttu-id="2dfd4-166">tooensure são toohello tooconnect capaz de internet da sua configuração de IP secundária através de IP público Olá associados-lo, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="2dfd4-167">Para configurações de IP secundárias, só pode ping toohello Internet se a configuração de Olá tem um endereço IP público com associados.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="2dfd4-168">Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="2dfd4-169">Para VMs com Linux, quando tentar toovalidate conectividade de saída de uma NIC secundária, poderá ser necessário tooadd de rotas adequado.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="2dfd4-170">Existem muitas formas toodo isto.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-170">There are many ways toodo this.</span></span> <span data-ttu-id="2dfd4-171">Consulte a documentação adequada para a distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="2dfd4-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="2dfd4-172">seguinte Olá é um método tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="2dfd4-173">Ser tooreplace se:</span><span class="sxs-lookup"><span data-stu-id="2dfd4-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="2dfd4-174">**10.0.0.5** com Olá privada endereço que tenha um IP público endereço IP associado tooit</span><span class="sxs-lookup"><span data-stu-id="2dfd4-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="2dfd4-175">**10.0.0.1** gateway predefinido de tooyour</span><span class="sxs-lookup"><span data-stu-id="2dfd4-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="2dfd4-176">**eth2** toohello nome do seu NIC secundário</span><span class="sxs-lookup"><span data-stu-id="2dfd4-176">**eth2** toohello name of your secondary NIC</span></span>
