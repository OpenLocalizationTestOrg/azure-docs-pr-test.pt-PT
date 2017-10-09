---
title: aaaSelecting nomes de utilizador do Linux | Microsoft Docs
description: "Saiba como nomes de utilizador tooselect para uma máquina virtual do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="f3eba-103">Selecionar Nomes de Utilizador para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="f3eba-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f3eba-104">Quando aprovisionar uma máquina virtual do Linux no Azure tem de especificar o nome de Olá de um utilizador não raiz que pode utilizar mais tarde toolog para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f3eba-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="f3eba-105">Pode optar por nome de Olá do novo utilizador de Olá, ou se Olá, aprovisionamento através do portal clássico do Azure pode aceitar a predefinição de Olá azureuser"nome".</span><span class="sxs-lookup"><span data-stu-id="f3eba-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="f3eba-106">Na maioria dos casos, este utilizador não existe na imagem base Olá e será criado durante o processo de aprovisionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="f3eba-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="f3eba-107">Se o utilizador Olá existe na imagem de VM base Olá, em seguida, agente Linux do Azure de Olá simplesmente configura palavra-passe de Olá e/ou a chave SSH para esse utilizador com base nas informações de Olá especificado ao criar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f3eba-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="f3eba-108">**No entanto**, Linux define um conjunto de nomes de utilizador que não deve ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="f3eba-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="f3eba-109">Olá irá do processo de aprovisionamento **falhar** se tentar tooprovision uma VM com Linux utilizando um utilizador existente de sistema, que é definido como um utilizador com UID 0 e 99.</span><span class="sxs-lookup"><span data-stu-id="f3eba-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="f3eba-110">Um exemplo típico é Olá `root` utilizador, que tem UID 0.</span><span class="sxs-lookup"><span data-stu-id="f3eba-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="f3eba-111">Consulte também: [Linux padrão Base - intervalos de ID de utilizador](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="f3eba-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="f3eba-112">Olá segue-se uma lista de utilizadores de sistema incorporada comuns para CentOS e Ubuntu que deve evitar utilizar quando aprovisionar uma máquina virtual do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3eba-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="f3eba-113">Esta lista é apenas um exemplo, consulte toohello documentação para a distribuição tooensure esse nome de utilizador Olá optar por não causar conflito com um utilizador existente do sistema.</span><span class="sxs-lookup"><span data-stu-id="f3eba-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="f3eba-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="f3eba-114">CentOS</span></span>
* <span data-ttu-id="f3eba-115">abrt</span><span class="sxs-lookup"><span data-stu-id="f3eba-115">abrt</span></span>
* <span data-ttu-id="f3eba-116">ADM</span><span class="sxs-lookup"><span data-stu-id="f3eba-116">adm</span></span>
* <span data-ttu-id="f3eba-117">áudio</span><span class="sxs-lookup"><span data-stu-id="f3eba-117">audio</span></span>
* <span data-ttu-id="f3eba-118">Reciclagem</span><span class="sxs-lookup"><span data-stu-id="f3eba-118">bin</span></span>
* <span data-ttu-id="f3eba-119">CD-ROM</span><span class="sxs-lookup"><span data-stu-id="f3eba-119">cdrom</span></span>
* <span data-ttu-id="f3eba-120">cgred</span><span class="sxs-lookup"><span data-stu-id="f3eba-120">cgred</span></span>
* <span data-ttu-id="f3eba-121">daemon</span><span class="sxs-lookup"><span data-stu-id="f3eba-121">daemon</span></span>
* <span data-ttu-id="f3eba-122">dbus</span><span class="sxs-lookup"><span data-stu-id="f3eba-122">dbus</span></span>
* <span data-ttu-id="f3eba-123">dialout</span><span class="sxs-lookup"><span data-stu-id="f3eba-123">dialout</span></span>
* <span data-ttu-id="f3eba-124">DIP</span><span class="sxs-lookup"><span data-stu-id="f3eba-124">dip</span></span>
* <span data-ttu-id="f3eba-125">disco</span><span class="sxs-lookup"><span data-stu-id="f3eba-125">disk</span></span>
* <span data-ttu-id="f3eba-126">disquetes</span><span class="sxs-lookup"><span data-stu-id="f3eba-126">floppy</span></span>
* <span data-ttu-id="f3eba-127">FTP</span><span class="sxs-lookup"><span data-stu-id="f3eba-127">ftp</span></span>
* <span data-ttu-id="f3eba-128">FTP</span><span class="sxs-lookup"><span data-stu-id="f3eba-128">ftp</span></span>
* <span data-ttu-id="f3eba-129">jogos</span><span class="sxs-lookup"><span data-stu-id="f3eba-129">games</span></span>
* <span data-ttu-id="f3eba-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="f3eba-130">gopher</span></span>
* <span data-ttu-id="f3eba-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="f3eba-131">haldaemon</span></span>
* <span data-ttu-id="f3eba-132">parar</span><span class="sxs-lookup"><span data-stu-id="f3eba-132">halt</span></span>
* <span data-ttu-id="f3eba-133">kmem</span><span class="sxs-lookup"><span data-stu-id="f3eba-133">kmem</span></span>
* <span data-ttu-id="f3eba-134">bloqueio</span><span class="sxs-lookup"><span data-stu-id="f3eba-134">lock</span></span>
* <span data-ttu-id="f3eba-135">LP</span><span class="sxs-lookup"><span data-stu-id="f3eba-135">lp</span></span>
* <span data-ttu-id="f3eba-136">capacidade de correio</span><span class="sxs-lookup"><span data-stu-id="f3eba-136">mail</span></span>
* <span data-ttu-id="f3eba-137">Man</span><span class="sxs-lookup"><span data-stu-id="f3eba-137">man</span></span>
* <span data-ttu-id="f3eba-138">memória</span><span class="sxs-lookup"><span data-stu-id="f3eba-138">mem</span></span>
* <span data-ttu-id="f3eba-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="f3eba-139">nfsnobody</span></span>
* <span data-ttu-id="f3eba-140">ninguém</span><span class="sxs-lookup"><span data-stu-id="f3eba-140">nobody</span></span>
* <span data-ttu-id="f3eba-141">NTP</span><span class="sxs-lookup"><span data-stu-id="f3eba-141">ntp</span></span>
* <span data-ttu-id="f3eba-142">operador</span><span class="sxs-lookup"><span data-stu-id="f3eba-142">operator</span></span>
* <span data-ttu-id="f3eba-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="f3eba-143">oprofile</span></span>
* <span data-ttu-id="f3eba-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="f3eba-144">postdrop</span></span>
* <span data-ttu-id="f3eba-145">sufixo</span><span class="sxs-lookup"><span data-stu-id="f3eba-145">postfix</span></span>
* <span data-ttu-id="f3eba-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="f3eba-146">qpidd</span></span>
* <span data-ttu-id="f3eba-147">raiz</span><span class="sxs-lookup"><span data-stu-id="f3eba-147">root</span></span>
* <span data-ttu-id="f3eba-148">RPC</span><span class="sxs-lookup"><span data-stu-id="f3eba-148">rpc</span></span>
* <span data-ttu-id="f3eba-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="f3eba-149">rpcuser</span></span>
* <span data-ttu-id="f3eba-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="f3eba-150">saslauth</span></span>
* <span data-ttu-id="f3eba-151">Encerramento</span><span class="sxs-lookup"><span data-stu-id="f3eba-151">shutdown</span></span>
* <span data-ttu-id="f3eba-152">slocate</span><span class="sxs-lookup"><span data-stu-id="f3eba-152">slocate</span></span>
* <span data-ttu-id="f3eba-153">sshd</span><span class="sxs-lookup"><span data-stu-id="f3eba-153">sshd</span></span>
* <span data-ttu-id="f3eba-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="f3eba-154">stapdev</span></span>
* <span data-ttu-id="f3eba-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="f3eba-155">stapusr</span></span>
* <span data-ttu-id="f3eba-156">Sincronização</span><span class="sxs-lookup"><span data-stu-id="f3eba-156">sync</span></span>
* <span data-ttu-id="f3eba-157">SYS</span><span class="sxs-lookup"><span data-stu-id="f3eba-157">sys</span></span>
* <span data-ttu-id="f3eba-158">banda</span><span class="sxs-lookup"><span data-stu-id="f3eba-158">tape</span></span>
* <span data-ttu-id="f3eba-159">Teste</span><span class="sxs-lookup"><span data-stu-id="f3eba-159">test</span></span>
* <span data-ttu-id="f3eba-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="f3eba-160">tcpdump</span></span>
* <span data-ttu-id="f3eba-161">TTY</span><span class="sxs-lookup"><span data-stu-id="f3eba-161">tty</span></span>
* <span data-ttu-id="f3eba-162">utilizadores</span><span class="sxs-lookup"><span data-stu-id="f3eba-162">users</span></span>
* <span data-ttu-id="f3eba-163">utempter</span><span class="sxs-lookup"><span data-stu-id="f3eba-163">utempter</span></span>
* <span data-ttu-id="f3eba-164">utmp</span><span class="sxs-lookup"><span data-stu-id="f3eba-164">utmp</span></span>
* <span data-ttu-id="f3eba-165">UUCP</span><span class="sxs-lookup"><span data-stu-id="f3eba-165">uucp</span></span>
* <span data-ttu-id="f3eba-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="f3eba-166">vcsa</span></span>
* <span data-ttu-id="f3eba-167">vídeo</span><span class="sxs-lookup"><span data-stu-id="f3eba-167">video</span></span>
* <span data-ttu-id="f3eba-168">roda</span><span class="sxs-lookup"><span data-stu-id="f3eba-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="f3eba-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f3eba-169">Ubuntu</span></span>
* <span data-ttu-id="f3eba-170">ADM</span><span class="sxs-lookup"><span data-stu-id="f3eba-170">adm</span></span>
* <span data-ttu-id="f3eba-171">Admin</span><span class="sxs-lookup"><span data-stu-id="f3eba-171">admin</span></span>
* <span data-ttu-id="f3eba-172">áudio</span><span class="sxs-lookup"><span data-stu-id="f3eba-172">audio</span></span>
* <span data-ttu-id="f3eba-173">cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="f3eba-173">backup</span></span>
* <span data-ttu-id="f3eba-174">Reciclagem</span><span class="sxs-lookup"><span data-stu-id="f3eba-174">bin</span></span>
* <span data-ttu-id="f3eba-175">CD-ROM</span><span class="sxs-lookup"><span data-stu-id="f3eba-175">cdrom</span></span>
* <span data-ttu-id="f3eba-176">crontab</span><span class="sxs-lookup"><span data-stu-id="f3eba-176">crontab</span></span>
* <span data-ttu-id="f3eba-177">daemon</span><span class="sxs-lookup"><span data-stu-id="f3eba-177">daemon</span></span>
* <span data-ttu-id="f3eba-178">dialout</span><span class="sxs-lookup"><span data-stu-id="f3eba-178">dialout</span></span>
* <span data-ttu-id="f3eba-179">DIP</span><span class="sxs-lookup"><span data-stu-id="f3eba-179">dip</span></span>
* <span data-ttu-id="f3eba-180">disco</span><span class="sxs-lookup"><span data-stu-id="f3eba-180">disk</span></span>
* <span data-ttu-id="f3eba-181">Fax</span><span class="sxs-lookup"><span data-stu-id="f3eba-181">fax</span></span>
* <span data-ttu-id="f3eba-182">disquetes</span><span class="sxs-lookup"><span data-stu-id="f3eba-182">floppy</span></span>
* <span data-ttu-id="f3eba-183">fuse</span><span class="sxs-lookup"><span data-stu-id="f3eba-183">fuse</span></span>
* <span data-ttu-id="f3eba-184">jogos</span><span class="sxs-lookup"><span data-stu-id="f3eba-184">games</span></span>
* <span data-ttu-id="f3eba-185">gnats</span><span class="sxs-lookup"><span data-stu-id="f3eba-185">gnats</span></span>
* <span data-ttu-id="f3eba-186">IRC</span><span class="sxs-lookup"><span data-stu-id="f3eba-186">irc</span></span>
* <span data-ttu-id="f3eba-187">kmem</span><span class="sxs-lookup"><span data-stu-id="f3eba-187">kmem</span></span>
* <span data-ttu-id="f3eba-188">horizontal</span><span class="sxs-lookup"><span data-stu-id="f3eba-188">landscape</span></span>
* <span data-ttu-id="f3eba-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="f3eba-189">libuuid</span></span>
* <span data-ttu-id="f3eba-190">lista</span><span class="sxs-lookup"><span data-stu-id="f3eba-190">list</span></span>
* <span data-ttu-id="f3eba-191">LP</span><span class="sxs-lookup"><span data-stu-id="f3eba-191">lp</span></span>
* <span data-ttu-id="f3eba-192">capacidade de correio</span><span class="sxs-lookup"><span data-stu-id="f3eba-192">mail</span></span>
* <span data-ttu-id="f3eba-193">Man</span><span class="sxs-lookup"><span data-stu-id="f3eba-193">man</span></span>
* <span data-ttu-id="f3eba-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="f3eba-194">messagebus</span></span>
* <span data-ttu-id="f3eba-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="f3eba-195">mlocate</span></span>
* <span data-ttu-id="f3eba-196">netdev</span><span class="sxs-lookup"><span data-stu-id="f3eba-196">netdev</span></span>
* <span data-ttu-id="f3eba-197">Notícias de última hora</span><span class="sxs-lookup"><span data-stu-id="f3eba-197">news</span></span>
* <span data-ttu-id="f3eba-198">ninguém</span><span class="sxs-lookup"><span data-stu-id="f3eba-198">nobody</span></span>
* <span data-ttu-id="f3eba-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="f3eba-199">nogroup</span></span>
* <span data-ttu-id="f3eba-200">operador</span><span class="sxs-lookup"><span data-stu-id="f3eba-200">operator</span></span>
* <span data-ttu-id="f3eba-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="f3eba-201">plugdev</span></span>
* <span data-ttu-id="f3eba-202">Proxy</span><span class="sxs-lookup"><span data-stu-id="f3eba-202">proxy</span></span>
* <span data-ttu-id="f3eba-203">raiz</span><span class="sxs-lookup"><span data-stu-id="f3eba-203">root</span></span>
* <span data-ttu-id="f3eba-204">SASL</span><span class="sxs-lookup"><span data-stu-id="f3eba-204">sasl</span></span>
* <span data-ttu-id="f3eba-205">sombra de volumes</span><span class="sxs-lookup"><span data-stu-id="f3eba-205">shadow</span></span>
* <span data-ttu-id="f3eba-206">SRC</span><span class="sxs-lookup"><span data-stu-id="f3eba-206">src</span></span>
* <span data-ttu-id="f3eba-207">SSH</span><span class="sxs-lookup"><span data-stu-id="f3eba-207">ssh</span></span>
* <span data-ttu-id="f3eba-208">sshd</span><span class="sxs-lookup"><span data-stu-id="f3eba-208">sshd</span></span>
* <span data-ttu-id="f3eba-209">funcionários</span><span class="sxs-lookup"><span data-stu-id="f3eba-209">staff</span></span>
* <span data-ttu-id="f3eba-210">sudo</span><span class="sxs-lookup"><span data-stu-id="f3eba-210">sudo</span></span>
* <span data-ttu-id="f3eba-211">Sincronização</span><span class="sxs-lookup"><span data-stu-id="f3eba-211">sync</span></span>
* <span data-ttu-id="f3eba-212">SYS</span><span class="sxs-lookup"><span data-stu-id="f3eba-212">sys</span></span>
* <span data-ttu-id="f3eba-213">syslog</span><span class="sxs-lookup"><span data-stu-id="f3eba-213">syslog</span></span>
* <span data-ttu-id="f3eba-214">banda</span><span class="sxs-lookup"><span data-stu-id="f3eba-214">tape</span></span>
* <span data-ttu-id="f3eba-215">TTY</span><span class="sxs-lookup"><span data-stu-id="f3eba-215">tty</span></span>
* <span data-ttu-id="f3eba-216">utilizadores</span><span class="sxs-lookup"><span data-stu-id="f3eba-216">users</span></span>
* <span data-ttu-id="f3eba-217">utmp</span><span class="sxs-lookup"><span data-stu-id="f3eba-217">utmp</span></span>
* <span data-ttu-id="f3eba-218">UUCP</span><span class="sxs-lookup"><span data-stu-id="f3eba-218">uucp</span></span>
* <span data-ttu-id="f3eba-219">vídeo</span><span class="sxs-lookup"><span data-stu-id="f3eba-219">video</span></span>
* <span data-ttu-id="f3eba-220">voz</span><span class="sxs-lookup"><span data-stu-id="f3eba-220">voice</span></span>
* <span data-ttu-id="f3eba-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="f3eba-221">whoopsie</span></span>
* <span data-ttu-id="f3eba-222">dados de www</span><span class="sxs-lookup"><span data-stu-id="f3eba-222">www-data</span></span>

