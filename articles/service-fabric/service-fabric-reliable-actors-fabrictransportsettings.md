---
title: Change FabricTransport settings in Azure microservices | Microsoft Docs
description: Learn about configuring Azure Service Fabric actor communication settings.
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: ''
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/22/2016
ms.author: suchia
ms.openlocfilehash: 4cbca6e496135a312bf4704dd0989f45dcccfc00
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549554"
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="b2d6c-103">Configure FabricTransport settings for Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b2d6c-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="b2d6c-104">Here are the settings that you can configure:</span><span class="sxs-lookup"><span data-stu-id="b2d6c-104">Here are the settings that you can configure:</span></span>

- <span data-ttu-id="b2d6c-105">C#: [FabricTansportSettings](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.services.communication.fabrictransport.common.fabrictransportsettings)</span><span class="sxs-lookup"><span data-stu-id="b2d6c-105">C#: [FabricTansportSettings](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.services.communication.fabrictransport.common.fabrictransportsettings)</span></span>
- <span data-ttu-id="b2d6c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="b2d6c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="b2d6c-107">You can modify the default configuration of FabricTransport in following ways.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="b2d6c-108">Assembly attribute</span><span class="sxs-lookup"><span data-stu-id="b2d6c-108">Assembly attribute</span></span>

<span data-ttu-id="b2d6c-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="b2d6c-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span><span class="sxs-lookup"><span data-stu-id="b2d6c-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

<span data-ttu-id="b2d6c-111">The following example shows how to change the default values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds:</span><span class="sxs-lookup"><span data-stu-id="b2d6c-111">The following example shows how to change the default values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="b2d6c-112">Config package</span><span class="sxs-lookup"><span data-stu-id="b2d6c-112">Config package</span></span>

<span data-ttu-id="b2d6c-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="b2d6c-114">Configure FabricTransport settings for the actor service</span><span class="sxs-lookup"><span data-stu-id="b2d6c-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="b2d6c-115">Add a TransportSettings section in the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="b2d6c-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="b2d6c-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="b2d6c-117">If that's not found, it checks for SectionName as "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="b2d6c-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="b2d6c-118">Configure FabricTransport settings for the actor client assembly</span><span class="sxs-lookup"><span data-stu-id="b2d6c-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="b2d6c-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="b2d6c-120">Then add a TransportSettings section in that file.</span><span class="sxs-lookup"><span data-stu-id="b2d6c-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="b2d6c-121">SectionName should be "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="b2d6c-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```
