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
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/23/2018
ms.author: subramar
ms.openlocfilehash: fd80784b899a51cf3c1f66842ce1e32ebddf0425
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782878"
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="07a75-103">Specify resources in a service manifest</span><span class="sxs-lookup"><span data-stu-id="07a75-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="07a75-104">Overview</span><span class="sxs-lookup"><span data-stu-id="07a75-104">Overview</span></span>
<span data-ttu-id="07a75-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span><span class="sxs-lookup"><span data-stu-id="07a75-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="07a75-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span><span class="sxs-lookup"><span data-stu-id="07a75-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="07a75-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="07a75-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="07a75-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span><span class="sxs-lookup"><span data-stu-id="07a75-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="07a75-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="07a75-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="07a75-110">Endpoints</span><span class="sxs-lookup"><span data-stu-id="07a75-110">Endpoints</span></span>
<span data-ttu-id="07a75-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span><span class="sxs-lookup"><span data-stu-id="07a75-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="07a75-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span><span class="sxs-lookup"><span data-stu-id="07a75-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="07a75-113">Additionally, services can also request a specific port in a resource.</span><span class="sxs-lookup"><span data-stu-id="07a75-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="07a75-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span><span class="sxs-lookup"><span data-stu-id="07a75-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="07a75-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span><span class="sxs-lookup"><span data-stu-id="07a75-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="07a75-116">If there are multiple code packages in a single service package, then the code package also needs to be referenced in the **Endpoints** section.</span><span class="sxs-lookup"><span data-stu-id="07a75-116">If there are multiple code packages in a single service package, then the code package also needs to be referenced in the **Endpoints** section.</span></span>  <span data-ttu-id="07a75-117">For example, if **ServiceEndpoint2a** and **ServiceEndpoint2b** are endpoints from the same service package referencing different code packages, the code package corresponding to each endpoint is clarified as follows:</span><span class="sxs-lookup"><span data-stu-id="07a75-117">For example, if **ServiceEndpoint2a** and **ServiceEndpoint2b** are endpoints from the same service package referencing different code packages, the code package corresponding to each endpoint is clarified as follows:</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint2a" Protocol="http" Port="802" CodePackageRef="Code1"/>
    <Endpoint Name="ServiceEndpoint2b" Protocol="http" Port="801" CodePackageRef="Code2"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="07a75-118">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="07a75-118">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="07a75-119">Example: specifying an HTTP endpoint for your service</span><span class="sxs-lookup"><span data-stu-id="07a75-119">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="07a75-120">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span><span class="sxs-lookup"><span data-stu-id="07a75-120">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="07a75-121">HTTP endpoints are automatically ACL'd by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="07a75-121">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="07a75-122">Example: specifying an HTTPS endpoint for your service</span><span class="sxs-lookup"><span data-stu-id="07a75-122">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="07a75-123">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span><span class="sxs-lookup"><span data-stu-id="07a75-123">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="07a75-124">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="07a75-124">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="07a75-125">A service’s protocol cannot be changed during application upgrade.</span><span class="sxs-lookup"><span data-stu-id="07a75-125">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="07a75-126">If it is changed during upgrade, it is a breaking change.</span><span class="sxs-lookup"><span data-stu-id="07a75-126">If it is changed during upgrade, it is a breaking change.</span></span>
> 

> [!WARNING] 
> <span data-ttu-id="07a75-127">When using HTTPS, do not use the same port and certificate for different service instances (independant of the application) deployed to the same node.</span><span class="sxs-lookup"><span data-stu-id="07a75-127">When using HTTPS, do not use the same port and certificate for different service instances (independant of the application) deployed to the same node.</span></span> <span data-ttu-id="07a75-128">Upgrading two different services using the same port in different application instances will result in an upgrade failure.</span><span class="sxs-lookup"><span data-stu-id="07a75-128">Upgrading two different services using the same port in different application instances will result in an upgrade failure.</span></span> <span data-ttu-id="07a75-129">For more information, see [Upgrading multiple applications with HTTPS endpoints ](service-fabric-application-upgrade.md#upgrading-multiple-applications-with-https-endpoints).</span><span class="sxs-lookup"><span data-stu-id="07a75-129">For more information, see [Upgrading multiple applications with HTTPS endpoints ](service-fabric-application-upgrade.md#upgrading-multiple-applications-with-https-endpoints).</span></span>
>

<span data-ttu-id="07a75-130">Here is an example ApplicationManifest that you need to set for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="07a75-130">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="07a75-131">The thumbprint for your certificate must be provided.</span><span class="sxs-lookup"><span data-stu-id="07a75-131">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="07a75-132">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="07a75-132">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="07a75-133">You can add more than one EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="07a75-133">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
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
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

<span data-ttu-id="07a75-134">For Linux clusters, the **MY** store defaults to the folder **/var/lib/sfcerts**.</span><span class="sxs-lookup"><span data-stu-id="07a75-134">For Linux clusters, the **MY** store defaults to the folder **/var/lib/sfcerts**.</span></span>


## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="07a75-135">Overriding Endpoints in ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="07a75-135">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="07a75-136">In the ApplicationManifest add a ResourceOverrides section, which will be a sibling to ConfigOverrides section.</span><span class="sxs-lookup"><span data-stu-id="07a75-136">In the ApplicationManifest add a ResourceOverrides section, which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="07a75-137">In this section, you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span><span class="sxs-lookup"><span data-stu-id="07a75-137">In this section, you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span> <span data-ttu-id="07a75-138">Overriding endpoints is supported in runtime 5.7.217/SDK 2.7.217 and higher.</span><span class="sxs-lookup"><span data-stu-id="07a75-138">Overriding endpoints is supported in runtime 5.7.217/SDK 2.7.217 and higher.</span></span>

<span data-ttu-id="07a75-139">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span><span class="sxs-lookup"><span data-stu-id="07a75-139">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="07a75-140">In the ServiceManifestImport section, add a new section "ResourceOverrides".</span><span class="sxs-lookup"><span data-stu-id="07a75-140">In the ServiceManifestImport section, add a new section "ResourceOverrides".</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="07a75-141">In the Parameters add below:</span><span class="sxs-lookup"><span data-stu-id="07a75-141">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="07a75-142">While deploying the application you can pass in these values as ApplicationParameters.</span><span class="sxs-lookup"><span data-stu-id="07a75-142">While deploying the application you can pass in these values as ApplicationParameters.</span></span>  <span data-ttu-id="07a75-143">For example:</span><span class="sxs-lookup"><span data-stu-id="07a75-143">For example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="07a75-144">Note: If the values provide for the ApplicationParameters is empty, we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span><span class="sxs-lookup"><span data-stu-id="07a75-144">Note: If the values provide for the ApplicationParameters is empty, we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="07a75-145">For example:</span><span class="sxs-lookup"><span data-stu-id="07a75-145">For example:</span></span>

<span data-ttu-id="07a75-146">If in the ServiceManifest you specified</span><span class="sxs-lookup"><span data-stu-id="07a75-146">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="07a75-147">And the Port1 and Protocol1 value for Application parameters is null or empty.</span><span class="sxs-lookup"><span data-stu-id="07a75-147">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="07a75-148">The port is still decided by ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="07a75-148">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="07a75-149">And the Protocol will tcp.</span><span class="sxs-lookup"><span data-stu-id="07a75-149">And the Protocol will tcp.</span></span>

<span data-ttu-id="07a75-150">Suppose you specify a wrong value.</span><span class="sxs-lookup"><span data-stu-id="07a75-150">Suppose you specify a wrong value.</span></span> <span data-ttu-id="07a75-151">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span><span class="sxs-lookup"><span data-stu-id="07a75-151">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="07a75-152">The value specified is 'Foo' and required is 'int'.</span><span class="sxs-lookup"><span data-stu-id="07a75-152">The value specified is 'Foo' and required is 'int'.</span></span>
