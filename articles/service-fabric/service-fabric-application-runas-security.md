---
title: Run an Azure Service Fabric service under system and local security accounts | Microsoft Docs
description: Learn how to run a Service Fabric application under system and local security accounts.  Create security principals and apply the Run-As policy to securely run your services.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/29/2018
ms.author: mfussell
ms.openlocfilehash: 33ca23834f35e631c6943ec22a88f4fe3dc853e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827892"
---
# <a name="run-a-service-as-a-local-user-account-or-local-system-account"></a><span data-ttu-id="04874-104">Run a service as a local user account or local system account</span><span class="sxs-lookup"><span data-stu-id="04874-104">Run a service as a local user account or local system account</span></span>
<span data-ttu-id="04874-105">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span><span class="sxs-lookup"><span data-stu-id="04874-105">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="04874-106">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span><span class="sxs-lookup"><span data-stu-id="04874-106">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="04874-107">Service Fabric also provides the capability to run applications under a local user or system account.</span><span class="sxs-lookup"><span data-stu-id="04874-107">Service Fabric also provides the capability to run applications under a local user or system account.</span></span> <span data-ttu-id="04874-108">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="04874-108">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>  <span data-ttu-id="04874-109">If you're running Service Fabric on a Windows standalone cluster, you can run a service under [Active Directory domain accounts](service-fabric-run-service-as-ad-user-or-group.md) or [group managed service accounts](service-fabric-run-service-as-gmsa.md).</span><span class="sxs-lookup"><span data-stu-id="04874-109">If you're running Service Fabric on a Windows standalone cluster, you can run a service under [Active Directory domain accounts](service-fabric-run-service-as-ad-user-or-group.md) or [group managed service accounts](service-fabric-run-service-as-gmsa.md).</span></span>

<span data-ttu-id="04874-110">In the application manifest, you define the user accounts required to run services or secure resources in the **Principals** section.</span><span class="sxs-lookup"><span data-stu-id="04874-110">In the application manifest, you define the user accounts required to run services or secure resources in the **Principals** section.</span></span> <span data-ttu-id="04874-111">You can also define and create user groups so that one or more users can be managed together.</span><span class="sxs-lookup"><span data-stu-id="04874-111">You can also define and create user groups so that one or more users can be managed together.</span></span> <span data-ttu-id="04874-112">This is useful when there are multiple users for different service entry points and they need common privileges that are available at the group level.</span><span class="sxs-lookup"><span data-stu-id="04874-112">This is useful when there are multiple users for different service entry points and they need common privileges that are available at the group level.</span></span>  <span data-ttu-id="04874-113">The users are then referenced in a RunAs policy, which is applied to a specific service or all the services in the application.</span><span class="sxs-lookup"><span data-stu-id="04874-113">The users are then referenced in a RunAs policy, which is applied to a specific service or all the services in the application.</span></span> 

<span data-ttu-id="04874-114">By default, the RunAs policy is applied to the main entry point.</span><span class="sxs-lookup"><span data-stu-id="04874-114">By default, the RunAs policy is applied to the main entry point.</span></span>  <span data-ttu-id="04874-115">You can also apply a RunAs policy to the setup entry point, if you need to [run certain high-privilege setup operations under a system account](service-fabric-run-script-at-service-startup.md), or both main and setup entry points.</span><span class="sxs-lookup"><span data-stu-id="04874-115">You can also apply a RunAs policy to the setup entry point, if you need to [run certain high-privilege setup operations under a system account](service-fabric-run-script-at-service-startup.md), or both main and setup entry points.</span></span>  

> [!NOTE] 
> <span data-ttu-id="04874-116">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy**.</span><span class="sxs-lookup"><span data-stu-id="04874-116">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy**.</span></span>  <span data-ttu-id="04874-117">For more information, see [Assign a security access policy for HTTP and HTTPS endpoints](service-fabric-assign-policy-to-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="04874-117">For more information, see [Assign a security access policy for HTTP and HTTPS endpoints](service-fabric-assign-policy-to-endpoint.md).</span></span> 
>

## <a name="run-a-service-as-a-local-user"></a><span data-ttu-id="04874-118">Run a service as a local user</span><span class="sxs-lookup"><span data-stu-id="04874-118">Run a service as a local user</span></span>
<span data-ttu-id="04874-119">You can create a local user that can be used to help secure a service within the application.</span><span class="sxs-lookup"><span data-stu-id="04874-119">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="04874-120">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="04874-120">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="04874-121">By default, these accounts do not have the same names as those specified in the application manifest (for example, *Customer3* in the following application manifest example).</span><span class="sxs-lookup"><span data-stu-id="04874-121">By default, these accounts do not have the same names as those specified in the application manifest (for example, *Customer3* in the following application manifest example).</span></span> <span data-ttu-id="04874-122">Instead, they are dynamically generated and have random passwords.</span><span class="sxs-lookup"><span data-stu-id="04874-122">Instead, they are dynamically generated and have random passwords.</span></span>

<span data-ttu-id="04874-123">In the **RunAsPolicy** section for a **ServiceManifestImport**, specify the user account from the **Principals** section to run the service code package.</span><span class="sxs-lookup"><span data-stu-id="04874-123">In the **RunAsPolicy** section for a **ServiceManifestImport**, specify the user account from the **Principals** section to run the service code package.</span></span>  <span data-ttu-id="04874-124">The following example shows how to create a local user and apply a RunAs policy to the main entry point:</span><span class="sxs-lookup"><span data-stu-id="04874-124">The following example shows how to create a local user and apply a RunAs policy to the main entry point:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application7Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="Web1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Web1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main" />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>    
    <Service Name="Web1" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="Web1Type" InstanceCount="[Web1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
  <Principals>
    <Users>
      <User Name="Customer3" />
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="create-a-local-user-group"></a><span data-ttu-id="04874-125">Create a local user group</span><span class="sxs-lookup"><span data-stu-id="04874-125">Create a local user group</span></span>
<span data-ttu-id="04874-126">You can create user groups and add one or more users to the group.</span><span class="sxs-lookup"><span data-stu-id="04874-126">You can create user groups and add one or more users to the group.</span></span> <span data-ttu-id="04874-127">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span><span class="sxs-lookup"><span data-stu-id="04874-127">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="04874-128">The following application manifest example shows a local group named *LocalAdminGroup* that has administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="04874-128">The following application manifest example shows a local group named *LocalAdminGroup* that has administrator privileges.</span></span> <span data-ttu-id="04874-129">Two users, *Customer1* and *Customer2*, are made members of this local group.</span><span class="sxs-lookup"><span data-stu-id="04874-129">Two users, *Customer1* and *Customer2*, are made members of this local group.</span></span> <span data-ttu-id="04874-130">In the **ServiceManifestImport** section, a RunAs policy is applied to run the *Stateful1Pkg* code package as *Customer2*.</span><span class="sxs-lookup"><span data-stu-id="04874-130">In the **ServiceManifestImport** section, a RunAs policy is applied to run the *Stateful1Pkg* code package as *Customer2*.</span></span>  <span data-ttu-id="04874-131">Another RunAs policy is applied to run the *Web1Pkg* code package as *Customer1*.</span><span class="sxs-lookup"><span data-stu-id="04874-131">Another RunAs policy is applied to run the *Web1Pkg* code package as *Customer1*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application7Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Web1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <RunAsPolicy CodePackageRef="Code" UserRef="Customer2" EntryPointType="Main"/>
    </Policies>
  </ServiceManifestImport>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Web1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" EntryPointType="Main"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <Service Name="Stateful1" ServicePackageActivationMode="ExclusiveProcess">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
    <Service Name="Web1" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="Web1Type" InstanceCount="[Web1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
  <Principals>
    <Groups>
      <Group Name="LocalAdminGroup">
        <Membership>
          <SystemGroup Name="Administrators" />
        </Membership>
      </Group>
    </Groups>
    <Users>
      <User Name="Customer1">
        <MemberOf>
          <Group NameRef="LocalAdminGroup" />
        </MemberOf>
      </User>
      <User Name="Customer2">
        <MemberOf>
          <Group NameRef="LocalAdminGroup" />
        </MemberOf>
      </User>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="04874-132">Apply a default policy to all service code packages</span><span class="sxs-lookup"><span data-stu-id="04874-132">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="04874-133">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span><span class="sxs-lookup"><span data-stu-id="04874-133">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="04874-134">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span><span class="sxs-lookup"><span data-stu-id="04874-134">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="04874-135">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** user specified in the principals section.</span><span class="sxs-lookup"><span data-stu-id="04874-135">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** user specified in the principals section.</span></span>  <span data-ttu-id="04874-136">Supported account types are LocalUser, NetworkService, LocalSystem, and LocalService.</span><span class="sxs-lookup"><span data-stu-id="04874-136">Supported account types are LocalUser, NetworkService, LocalSystem, and LocalService.</span></span>  <span data-ttu-id="04874-137">If using a local user or service, also specify the account name and password.</span><span class="sxs-lookup"><span data-stu-id="04874-137">If using a local user or service, also specify the account name and password.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application7Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="Web1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Web1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    
  </ServiceManifestImport>
  <DefaultServices>    
    <Service Name="Web1" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="Web1Type" InstanceCount="[Web1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
  <Principals>
    <Users>
      <User Name="MyDefaultAccount" AccountType="NetworkService" />      
    </Users>
  </Principals>
  <Policies>
    <DefaultRunAsPolicy UserRef="MyDefaultAccount" />
  </Policies>
</ApplicationManifest>
```

## <a name="debug-a-code-package-locally-using-console-redirection"></a><span data-ttu-id="04874-138">Debug a code package locally using console redirection</span><span class="sxs-lookup"><span data-stu-id="04874-138">Debug a code package locally using console redirection</span></span>
<span data-ttu-id="04874-139">Occasionally, it's useful for debugging purposes to see the console output from a running service.</span><span class="sxs-lookup"><span data-stu-id="04874-139">Occasionally, it's useful for debugging purposes to see the console output from a running service.</span></span> <span data-ttu-id="04874-140">You can set a console redirection policy on the entry point in the service manifest, which writes the output to a file.</span><span class="sxs-lookup"><span data-stu-id="04874-140">You can set a console redirection policy on the entry point in the service manifest, which writes the output to a file.</span></span> <span data-ttu-id="04874-141">The file output is written to the application folder called **log** on the cluster node where the application is deployed and run.</span><span class="sxs-lookup"><span data-stu-id="04874-141">The file output is written to the application folder called **log** on the cluster node where the application is deployed and run.</span></span> 

> [!WARNING]
> <span data-ttu-id="04874-142">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span><span class="sxs-lookup"><span data-stu-id="04874-142">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="04874-143">*Only* use this for local development and debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="04874-143">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="04874-144">The following service manifest example shows enabling console redirection with a FileRetentionCount value:</span><span class="sxs-lookup"><span data-stu-id="04874-144">The following service manifest example shows enabling console redirection with a FileRetentionCount value:</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>VotingWeb.exe</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
        <ConsoleRedirection FileRetentionCount="10"/>
      </ExeHost>
    </EntryPoint>
</CodePackage>

```

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="04874-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="04874-145">Next steps</span></span>
* [<span data-ttu-id="04874-146">Understand the application model</span><span class="sxs-lookup"><span data-stu-id="04874-146">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="04874-147">Specify resources in a service manifest</span><span class="sxs-lookup"><span data-stu-id="04874-147">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="04874-148">Deploy an application</span><span class="sxs-lookup"><span data-stu-id="04874-148">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
