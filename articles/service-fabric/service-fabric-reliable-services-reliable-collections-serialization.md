---
title: "aaaReliable serialização do objeto de coleção no Service Fabric do Azure | Microsoft Docs"
description: "Serialização de objeto de coleções de fiável de recursos de infraestrutura de serviço do Azure"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="3bbbd-103">Fiável serialização do objeto de coleção no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3bbbd-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="3bbbd-104">As coleções fiável replicam e manter os seus toomake itens certificar de que são duráveis em falhas de máquina e falhas de energia.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="3bbbd-105">Os itens tooreplicate e toopersist, tooserialize necessidade de fiável coleções-los.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="3bbbd-106">Fiável coleções obter serializador adequado Olá para um determinado tipo de Gestor de estado fiável.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="3bbbd-107">Gestor de estado de fiável contém serializers incorporadas e permite toobe serializers personalizado registado para um determinado tipo.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="3bbbd-108">Serializers incorporadas</span><span class="sxs-lookup"><span data-stu-id="3bbbd-108">Built-in Serializers</span></span>

<span data-ttu-id="3bbbd-109">O Gestor de estado fiável inclui serializador incorporado para alguns tipos comuns, para que podem ser serializados de forma eficiente por predefinição.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="3bbbd-110">Para outros tipos, Gestor de estado fiável retrocede toouse Olá [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="3bbbd-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="3bbbd-111">Serializers incorporadas são mais eficientes, uma vez que já estão habituados não é possível alterar os respetivos tipos e não precisarem tooinclude informações sobre o tipo de Olá, como o respetivo nome de tipo.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="3bbbd-112">Gestor de estado de fiável tem serializador incorporado para tipos seguintes:</span><span class="sxs-lookup"><span data-stu-id="3bbbd-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="3bbbd-113">GUID</span><span class="sxs-lookup"><span data-stu-id="3bbbd-113">Guid</span></span>
- <span data-ttu-id="3bbbd-114">bool</span><span class="sxs-lookup"><span data-stu-id="3bbbd-114">bool</span></span>
- <span data-ttu-id="3bbbd-115">Bytes</span><span class="sxs-lookup"><span data-stu-id="3bbbd-115">byte</span></span>
- <span data-ttu-id="3bbbd-116">SByte</span><span class="sxs-lookup"><span data-stu-id="3bbbd-116">sbyte</span></span>
- <span data-ttu-id="3bbbd-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="3bbbd-117">byte[]</span></span>
- <span data-ttu-id="3bbbd-118">char</span><span class="sxs-lookup"><span data-stu-id="3bbbd-118">char</span></span>
- <span data-ttu-id="3bbbd-119">Cadeia</span><span class="sxs-lookup"><span data-stu-id="3bbbd-119">string</span></span>
- <span data-ttu-id="3bbbd-120">Decimal</span><span class="sxs-lookup"><span data-stu-id="3bbbd-120">decimal</span></span>
- <span data-ttu-id="3bbbd-121">duplo</span><span class="sxs-lookup"><span data-stu-id="3bbbd-121">double</span></span>
- <span data-ttu-id="3bbbd-122">Número de vírgula flutuante</span><span class="sxs-lookup"><span data-stu-id="3bbbd-122">float</span></span>
- <span data-ttu-id="3bbbd-123">Int</span><span class="sxs-lookup"><span data-stu-id="3bbbd-123">int</span></span>
- <span data-ttu-id="3bbbd-124">UInt</span><span class="sxs-lookup"><span data-stu-id="3bbbd-124">uint</span></span>
- <span data-ttu-id="3bbbd-125">longa</span><span class="sxs-lookup"><span data-stu-id="3bbbd-125">long</span></span>
- <span data-ttu-id="3bbbd-126">ulong</span><span class="sxs-lookup"><span data-stu-id="3bbbd-126">ulong</span></span>
- <span data-ttu-id="3bbbd-127">curto</span><span class="sxs-lookup"><span data-stu-id="3bbbd-127">short</span></span>
- <span data-ttu-id="3bbbd-128">ushort</span><span class="sxs-lookup"><span data-stu-id="3bbbd-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="3bbbd-129">Serialização personalizada</span><span class="sxs-lookup"><span data-stu-id="3bbbd-129">Custom Serialization</span></span>

<span data-ttu-id="3bbbd-130">Serializers personalizados são frequentemente utilizadas tooincrease desempenho ou tooencrypt Olá dados através de transmissão de Olá e no disco.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="3bbbd-131">Entre outras razões serializers personalizados são geralmente mais eficientes do que o serializador genérico, uma vez que não precisam de tooserialize informações sobre o tipo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="3bbbd-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) é tooregister utilizado um serializador personalizado para Olá tipo T. indicado Este registo deverá ocorrer na construção Olá de Olá StatefulServiceBase tooensure que, antes de inicia a recuperação, todas as coleções fiável têm acesso toohello serializador relevantes tooread os seus dados persistentes anteriores.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="3bbbd-133">Serializers personalizados são indicados precedência sobre serializers incorporadas.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="3bbbd-134">Por exemplo, quando é registado um serializador personalizado para int, é números inteiros de tooserialize utilizado em vez do serializador incorporada Olá para int.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="3bbbd-135">Como tooimplement um serializador personalizado</span><span class="sxs-lookup"><span data-stu-id="3bbbd-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="3bbbd-136">Necessita de um serializador personalizado tooimplement Olá [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="3bbbd-137">IStateSerializer<T> inclui uma sobrecarga escrita e leitura que leva uma T adicional chamado valor base.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="3bbbd-138">Esta API está para serialização diferencial.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-138">This API is for differential serialization.</span></span> <span data-ttu-id="3bbbd-139">Atualmente não está exposta a funcionalidade de serialização diferencial.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="3bbbd-140">Por conseguinte, estes dois sobrecargas não são denominadas até serialização diferencial está exposta e ativada.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="3bbbd-141">Segue-se um tipo personalizado de exemplo chamado OrderKey contém quatro propriedades</span><span class="sxs-lookup"><span data-stu-id="3bbbd-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="3bbbd-142">Segue-se uma implementação de exemplo do IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="3bbbd-143">Tenha em atenção que a leitura e escrita sobrecargas que utilizam no baseValue, chamar os seus respetiva sobrecarga para reencaminhamentos de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="3bbbd-144">Upgradability</span><span class="sxs-lookup"><span data-stu-id="3bbbd-144">Upgradability</span></span>
<span data-ttu-id="3bbbd-145">Num [a atualização da aplicação](service-fabric-application-upgrade.md), atualização Olá é aplicado tooa subconjunto de nós, um domínio de atualização a uma hora.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="3bbbd-146">Durante este processo, alguns domínios de atualização serão numa versão mais recente do Olá da sua aplicação e alguns domínios de atualização serão numa versão mais antiga do Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="3bbbd-147">Durante a implementação de Olá, versão nova do Olá da sua aplicação tem de ser capaz de tooread versão antiga do Olá dos seus dados e versão antiga do Olá da sua aplicação tem de ser capaz de tooread Olá nova versão, dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="3bbbd-148">Formato de dados de Olá não esteja com versões anteriores e reencaminhar atualização Olá compatível, podem falhar, worse, dados ou pode ser perdido ou corrompido.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="3bbbd-149">Se estiver a utilizar o serializador incorporado, não terá tooworry sobre a compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="3bbbd-150">No entanto, se estiver a utilizar um serializador personalizado ou Olá DataContractSerializer, dados de Olá tem toobe infinitamente efeitos e reencaminha compatíveis.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="3bbbd-151">Por outras palavras, cada versão do serializador tem tooserialize capaz de toobe e anular a serialização qualquer versão do tipo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="3bbbd-152">Os utilizadores de contrato de dados devem seguir as regras de controlo de versões bem definidos Olá para adicionar, remover e alteração dos campos.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="3bbbd-153">Contrato de dados também tem suporte para lidar com campos desconhecidos, hooking no processo de serialização e a anulação da serialização de Olá e lidar com a herança de classe.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="3bbbd-154">Para obter mais informações, consulte [através de contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bbbd-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="3bbbd-155">Utilizadores de serializador personalizado devem cumprir as diretrizes de toohello do serializador Olá estão a utilizar toomake se de que é efeitos e reencaminha compatível.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="3bbbd-156">Uma forma comum de oferecer suporte a todas as versões é adicionar informações de tamanho em início Olá e apenas adicionar propriedades opcionais.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="3bbbd-157">Desta forma pode ler cada versão como muito possa e ir ao longo da parte restante do Olá do fluxo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bbbd-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3bbbd-158">Next steps</span></span>
  * [<span data-ttu-id="3bbbd-159">Serialização e a atualização</span><span class="sxs-lookup"><span data-stu-id="3bbbd-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="3bbbd-160">Referência para programadores para coleções fiável</span><span class="sxs-lookup"><span data-stu-id="3bbbd-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="3bbbd-161">[Atualizar a aplicação utilizando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta-o através de uma atualização da aplicação com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="3bbbd-162">[Atualizar a sua aplicação através do Powershell](service-fabric-application-upgrade-tutorial-powershell.md) orienta-o através de uma atualização da aplicação através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bbbd-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="3bbbd-163">Controlar a forma como a aplicação atualiza utilizando [atualizar parâmetros](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="3bbbd-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="3bbbd-164">Saiba como toouse avançada funcionalidade ao atualizar a sua aplicação ao referir-se demasiado[tópicos avançados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="3bbbd-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="3bbbd-165">Resolva problemas comuns nas atualizações de aplicações ao referir-se passos toohello [resolução de problemas de atualizações de aplicação](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3bbbd-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
