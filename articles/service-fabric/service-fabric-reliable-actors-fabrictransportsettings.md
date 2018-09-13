---
title: Change FabricTransport settings in Azure Service Fabric actors | Microsoft Docs
description: Learn about configuring Azure Service Fabric actor communication settings.
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: ''
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: afe10ba7120cb16d9cd171811f7abf1fc861d642
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801182"
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="d711c-103">Configure FabricTransport settings for Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d711c-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="d711c-104">Here are the settings that you can configure:</span><span class="sxs-lookup"><span data-stu-id="d711c-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="d711c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="d711c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="d711c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="d711c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="d711c-107">You can modify the default configuration of FabricTransport in following ways.</span><span class="sxs-lookup"><span data-stu-id="d711c-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="d711c-108">Assembly attribute</span><span class="sxs-lookup"><span data-stu-id="d711c-108">Assembly attribute</span></span>

<span data-ttu-id="d711c-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span><span class="sxs-lookup"><span data-stu-id="d711c-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="d711c-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span><span class="sxs-lookup"><span data-stu-id="d711c-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="d711c-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="d711c-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="d711c-112">Config package</span><span class="sxs-lookup"><span data-stu-id="d711c-112">Config package</span></span>

<span data-ttu-id="d711c-113">You can use a [config package](service-fabric-application-and-service-manifests.md) to modify the default configuration.</span><span class="sxs-lookup"><span data-stu-id="d711c-113">You can use a [config package](service-fabric-application-and-service-manifests.md) to modify the default configuration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d711c-114">On Linux nodes, certificates must be PEM-formatted.</span><span class="sxs-lookup"><span data-stu-id="d711c-114">On Linux nodes, certificates must be PEM-formatted.</span></span> <span data-ttu-id="d711c-115">To learn more about locating and configuring certificates for Linux, see [Configure certificates on Linux](./service-fabric-configure-certificates-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d711c-115">To learn more about locating and configuring certificates for Linux, see [Configure certificates on Linux](./service-fabric-configure-certificates-linux.md).</span></span> 
> 

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="d711c-116">Configure FabricTransport settings for the actor service</span><span class="sxs-lookup"><span data-stu-id="d711c-116">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="d711c-117">Add a TransportSettings section in the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="d711c-117">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="d711c-118">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="d711c-118">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="d711c-119">If that's not found, it checks for SectionName as "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="d711c-119">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="d711c-120">Configure FabricTransport settings for the actor client assembly</span><span class="sxs-lookup"><span data-stu-id="d711c-120">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="d711c-121">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span><span class="sxs-lookup"><span data-stu-id="d711c-121">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="d711c-122">Then add a TransportSettings section in that file.</span><span class="sxs-lookup"><span data-stu-id="d711c-122">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="d711c-123">SectionName should be "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="d711c-123">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="d711c-124">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span><span class="sxs-lookup"><span data-stu-id="d711c-124">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="d711c-125">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="d711c-125">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="d711c-126">Below is the example for the Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="d711c-126">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="d711c-127">Below is the example for the Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="d711c-127">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="d711c-128">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span><span class="sxs-lookup"><span data-stu-id="d711c-128">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="d711c-129">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span><span class="sxs-lookup"><span data-stu-id="d711c-129">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="d711c-130">Below is the example for the Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="d711c-130">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="d711c-131">Below is the example for the Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="d711c-131">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
