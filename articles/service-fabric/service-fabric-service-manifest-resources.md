---
title: Specifying Service Fabric service endpoints | Microsoft Docs
description: How to describe endpoint resources in a service manifest, including how to set up HTTPS endpoints
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: 9cfdb94d1e030fe9d467389acf8894d79efd17d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563707"
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="9795d-103">Specify resources in a service manifest</span><span class="sxs-lookup"><span data-stu-id="9795d-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="9795d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9795d-104">Overview</span></span>
<span data-ttu-id="9795d-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span><span class="sxs-lookup"><span data-stu-id="9795d-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="9795d-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span><span class="sxs-lookup"><span data-stu-id="9795d-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="9795d-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="9795d-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="9795d-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span><span class="sxs-lookup"><span data-stu-id="9795d-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="9795d-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="9795d-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="9795d-110">Endpoints</span><span class="sxs-lookup"><span data-stu-id="9795d-110">Endpoints</span></span>
<span data-ttu-id="9795d-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span><span class="sxs-lookup"><span data-stu-id="9795d-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="9795d-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span><span class="sxs-lookup"><span data-stu-id="9795d-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="9795d-113">Additionally, services can also request a specific port in a resource.</span><span class="sxs-lookup"><span data-stu-id="9795d-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="9795d-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span><span class="sxs-lookup"><span data-stu-id="9795d-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="9795d-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span><span class="sxs-lookup"><span data-stu-id="9795d-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="9795d-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="9795d-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="9795d-117">Example: specifying an HTTP endpoint for your service</span><span class="sxs-lookup"><span data-stu-id="9795d-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="9795d-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span><span class="sxs-lookup"><span data-stu-id="9795d-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="9795d-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9795d-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="9795d-120">Example: specifying an HTTPS endpoint for your service</span><span class="sxs-lookup"><span data-stu-id="9795d-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="9795d-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span><span class="sxs-lookup"><span data-stu-id="9795d-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="9795d-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="9795d-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="9795d-123">A service’s protocol cannot be changed during application upgrade.</span><span class="sxs-lookup"><span data-stu-id="9795d-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="9795d-124">If it is changed during upgrade, it is a breaking change.</span><span class="sxs-lookup"><span data-stu-id="9795d-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="9795d-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9795d-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="9795d-126">The thumbprint for your certificate must be provided.</span><span class="sxs-lookup"><span data-stu-id="9795d-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="9795d-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="9795d-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="9795d-128">You can add more than one EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="9795d-128">You can add more than one EndpointCertificate.</span></span>  

```
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="2" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```
