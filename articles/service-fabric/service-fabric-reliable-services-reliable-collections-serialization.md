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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Fiável serialização do objeto de coleção no Azure Service Fabric
As coleções fiável replicam e manter os seus toomake itens certificar de que são duráveis em falhas de máquina e falhas de energia.
Os itens tooreplicate e toopersist, tooserialize necessidade de fiável coleções-los.

Fiável coleções obter serializador adequado Olá para um determinado tipo de Gestor de estado fiável.
Gestor de estado de fiável contém serializers incorporadas e permite toobe serializers personalizado registado para um determinado tipo.

## <a name="built-in-serializers"></a>Serializers incorporadas

O Gestor de estado fiável inclui serializador incorporado para alguns tipos comuns, para que podem ser serializados de forma eficiente por predefinição. Para outros tipos, Gestor de estado fiável retrocede toouse Olá [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Serializers incorporadas são mais eficientes, uma vez que já estão habituados não é possível alterar os respetivos tipos e não precisarem tooinclude informações sobre o tipo de Olá, como o respetivo nome de tipo.

Gestor de estado de fiável tem serializador incorporado para tipos seguintes: 
- GUID
- bool
- Bytes
- SByte
- Byte]
- char
- Cadeia
- Decimal
- duplo
- Número de vírgula flutuante
- Int
- UInt
- longa
- ulong
- curto
- ushort

## <a name="custom-serialization"></a>Serialização personalizada

Serializers personalizados são frequentemente utilizadas tooincrease desempenho ou tooencrypt Olá dados através de transmissão de Olá e no disco. Entre outras razões serializers personalizados são geralmente mais eficientes do que o serializador genérico, uma vez que não precisam de tooserialize informações sobre o tipo de Olá. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) é tooregister utilizado um serializador personalizado para Olá tipo T. indicado Este registo deverá ocorrer na construção Olá de Olá StatefulServiceBase tooensure que, antes de inicia a recuperação, todas as coleções fiável têm acesso toohello serializador relevantes tooread os seus dados persistentes anteriores.

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
> Serializers personalizados são indicados precedência sobre serializers incorporadas. Por exemplo, quando é registado um serializador personalizado para int, é números inteiros de tooserialize utilizado em vez do serializador incorporada Olá para int.

### <a name="how-tooimplement-a-custom-serializer"></a>Como tooimplement um serializador personalizado

Necessita de um serializador personalizado tooimplement Olá [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.

> [!NOTE]
> IStateSerializer<T> inclui uma sobrecarga escrita e leitura que leva uma T adicional chamado valor base. Esta API está para serialização diferencial. Atualmente não está exposta a funcionalidade de serialização diferencial. Por conseguinte, estes dois sobrecargas não são denominadas até serialização diferencial está exposta e ativada.

Segue-se um tipo personalizado de exemplo chamado OrderKey contém quatro propriedades

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

Segue-se uma implementação de exemplo do IStateSerializer<OrderKey>.
Tenha em atenção que a leitura e escrita sobrecargas que utilizam no baseValue, chamar os seus respetiva sobrecarga para reencaminhamentos de compatibilidade.

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

## <a name="upgradability"></a>Upgradability
Num [a atualização da aplicação](service-fabric-application-upgrade.md), atualização Olá é aplicado tooa subconjunto de nós, um domínio de atualização a uma hora. Durante este processo, alguns domínios de atualização serão numa versão mais recente do Olá da sua aplicação e alguns domínios de atualização serão numa versão mais antiga do Olá da sua aplicação. Durante a implementação de Olá, versão nova do Olá da sua aplicação tem de ser capaz de tooread versão antiga do Olá dos seus dados e versão antiga do Olá da sua aplicação tem de ser capaz de tooread Olá nova versão, dos seus dados. Formato de dados de Olá não esteja com versões anteriores e reencaminhar atualização Olá compatível, podem falhar, worse, dados ou pode ser perdido ou corrompido.

Se estiver a utilizar o serializador incorporado, não terá tooworry sobre a compatibilidade.
No entanto, se estiver a utilizar um serializador personalizado ou Olá DataContractSerializer, dados de Olá tem toobe infinitamente efeitos e reencaminha compatíveis.
Por outras palavras, cada versão do serializador tem tooserialize capaz de toobe e anular a serialização qualquer versão do tipo de Olá.

Os utilizadores de contrato de dados devem seguir as regras de controlo de versões bem definidos Olá para adicionar, remover e alteração dos campos. Contrato de dados também tem suporte para lidar com campos desconhecidos, hooking no processo de serialização e a anulação da serialização de Olá e lidar com a herança de classe. Para obter mais informações, consulte [através de contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).

Utilizadores de serializador personalizado devem cumprir as diretrizes de toohello do serializador Olá estão a utilizar toomake se de que é efeitos e reencaminha compatível.
Uma forma comum de oferecer suporte a todas as versões é adicionar informações de tamanho em início Olá e apenas adicionar propriedades opcionais.
Desta forma pode ler cada versão como muito possa e ir ao longo da parte restante do Olá do fluxo de Olá.

## <a name="next-steps"></a>Passos seguintes
  * [Serialização e a atualização](service-fabric-application-upgrade-data-serialization.md)
  * [Referência para programadores para coleções fiável](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Atualizar a aplicação utilizando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta-o através de uma atualização da aplicação com o Visual Studio.
  * [Atualizar a sua aplicação através do Powershell](service-fabric-application-upgrade-tutorial-powershell.md) orienta-o através de uma atualização da aplicação através do PowerShell.
  * Controlar a forma como a aplicação atualiza utilizando [atualizar parâmetros](service-fabric-application-upgrade-parameters.md).
  * Saiba como toouse avançada funcionalidade ao atualizar a sua aplicação ao referir-se demasiado[tópicos avançados](service-fabric-application-upgrade-advanced.md).
  * Resolva problemas comuns nas atualizações de aplicações ao referir-se passos toohello [resolução de problemas de atualizações de aplicação](service-fabric-application-upgrade-troubleshooting.md).
