---
title: Cloud Services Role config XPath cheat sheet | Microsoft Docs
description: The various XPath settings you can use in the cloud service role config to expose settings as an environment variable.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671248"
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="c2cd9-103">Expose role configuration settings as an environment variable with XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="c2cd9-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="c2cd9-105">The following XPath values are supported (which correspond to API values).</span><span class="sxs-lookup"><span data-stu-id="c2cd9-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="c2cd9-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="c2cd9-107">App running in emulator</span><span class="sxs-lookup"><span data-stu-id="c2cd9-107">App running in emulator</span></span>
<span data-ttu-id="c2cd9-108">Indicates that the app is running in the emulator.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="c2cd9-109">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-109">Type</span></span> | <span data-ttu-id="c2cd9-110">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-111">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-111">XPath</span></span> |<span data-ttu-id="c2cd9-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="c2cd9-113">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-113">Code</span></span> |<span data-ttu-id="c2cd9-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="c2cd9-115">Deployment ID</span><span class="sxs-lookup"><span data-stu-id="c2cd9-115">Deployment ID</span></span>
<span data-ttu-id="c2cd9-116">Retrieves the deployment ID for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="c2cd9-117">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-117">Type</span></span> | <span data-ttu-id="c2cd9-118">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-119">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-119">XPath</span></span> |<span data-ttu-id="c2cd9-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="c2cd9-121">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-121">Code</span></span> |<span data-ttu-id="c2cd9-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="c2cd9-123">Role ID</span><span class="sxs-lookup"><span data-stu-id="c2cd9-123">Role ID</span></span>
<span data-ttu-id="c2cd9-124">Retrieves the current role ID for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="c2cd9-125">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-125">Type</span></span> | <span data-ttu-id="c2cd9-126">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-127">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-127">XPath</span></span> |<span data-ttu-id="c2cd9-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="c2cd9-129">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-129">Code</span></span> |<span data-ttu-id="c2cd9-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="c2cd9-131">Update domain</span><span class="sxs-lookup"><span data-stu-id="c2cd9-131">Update domain</span></span>
<span data-ttu-id="c2cd9-132">Retrieves the update domain of the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="c2cd9-133">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-133">Type</span></span> | <span data-ttu-id="c2cd9-134">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-135">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-135">XPath</span></span> |<span data-ttu-id="c2cd9-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="c2cd9-137">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-137">Code</span></span> |<span data-ttu-id="c2cd9-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="c2cd9-139">Fault domain</span><span class="sxs-lookup"><span data-stu-id="c2cd9-139">Fault domain</span></span>
<span data-ttu-id="c2cd9-140">Retrieves the fault domain of the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="c2cd9-141">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-141">Type</span></span> | <span data-ttu-id="c2cd9-142">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-143">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-143">XPath</span></span> |<span data-ttu-id="c2cd9-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="c2cd9-145">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-145">Code</span></span> |<span data-ttu-id="c2cd9-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="c2cd9-147">Role name</span><span class="sxs-lookup"><span data-stu-id="c2cd9-147">Role name</span></span>
<span data-ttu-id="c2cd9-148">Retrieves the role name of the instances.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="c2cd9-149">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-149">Type</span></span> | <span data-ttu-id="c2cd9-150">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-151">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-151">XPath</span></span> |<span data-ttu-id="c2cd9-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="c2cd9-153">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-153">Code</span></span> |<span data-ttu-id="c2cd9-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="c2cd9-155">Config setting</span><span class="sxs-lookup"><span data-stu-id="c2cd9-155">Config setting</span></span>
<span data-ttu-id="c2cd9-156">Retrieves the value of the specified configuration setting.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="c2cd9-157">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-157">Type</span></span> | <span data-ttu-id="c2cd9-158">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-159">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-159">XPath</span></span> |<span data-ttu-id="c2cd9-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="c2cd9-161">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-161">Code</span></span> |<span data-ttu-id="c2cd9-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="c2cd9-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="c2cd9-163">Local storage path</span><span class="sxs-lookup"><span data-stu-id="c2cd9-163">Local storage path</span></span>
<span data-ttu-id="c2cd9-164">Retrieves the local storage path for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="c2cd9-165">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-165">Type</span></span> | <span data-ttu-id="c2cd9-166">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-167">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-167">XPath</span></span> |<span data-ttu-id="c2cd9-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="c2cd9-169">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-169">Code</span></span> |<span data-ttu-id="c2cd9-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="c2cd9-171">Local storage size</span><span class="sxs-lookup"><span data-stu-id="c2cd9-171">Local storage size</span></span>
<span data-ttu-id="c2cd9-172">Retrieves the size of the local storage for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="c2cd9-173">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-173">Type</span></span> | <span data-ttu-id="c2cd9-174">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-175">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-175">XPath</span></span> |<span data-ttu-id="c2cd9-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="c2cd9-177">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-177">Code</span></span> |<span data-ttu-id="c2cd9-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="c2cd9-179">Endpoint protocol</span><span class="sxs-lookup"><span data-stu-id="c2cd9-179">Endpoint protocol</span></span>
<span data-ttu-id="c2cd9-180">Retrieves the endpoint protocol for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="c2cd9-181">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-181">Type</span></span> | <span data-ttu-id="c2cd9-182">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-183">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-183">XPath</span></span> |<span data-ttu-id="c2cd9-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="c2cd9-185">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-185">Code</span></span> |<span data-ttu-id="c2cd9-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="c2cd9-187">Endpoint IP</span><span class="sxs-lookup"><span data-stu-id="c2cd9-187">Endpoint IP</span></span>
<span data-ttu-id="c2cd9-188">Gets the specified endpoint's IP address.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="c2cd9-189">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-189">Type</span></span> | <span data-ttu-id="c2cd9-190">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-191">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-191">XPath</span></span> |<span data-ttu-id="c2cd9-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="c2cd9-193">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-193">Code</span></span> |<span data-ttu-id="c2cd9-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="c2cd9-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="c2cd9-195">Endpoint port</span><span class="sxs-lookup"><span data-stu-id="c2cd9-195">Endpoint port</span></span>
<span data-ttu-id="c2cd9-196">Retrieves the endpoint port for the instance.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="c2cd9-197">Type</span><span class="sxs-lookup"><span data-stu-id="c2cd9-197">Type</span></span> | <span data-ttu-id="c2cd9-198">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c2cd9-199">XPath</span><span class="sxs-lookup"><span data-stu-id="c2cd9-199">XPath</span></span> |<span data-ttu-id="c2cd9-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="c2cd9-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="c2cd9-201">Code</span><span class="sxs-lookup"><span data-stu-id="c2cd9-201">Code</span></span> |<span data-ttu-id="c2cd9-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="c2cd9-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="c2cd9-203">Example</span><span class="sxs-lookup"><span data-stu-id="c2cd9-203">Example</span></span>
<span data-ttu-id="c2cd9-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="c2cd9-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="c2cd9-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2cd9-205">Next steps</span></span>
<span data-ttu-id="c2cd9-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="c2cd9-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="c2cd9-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span><span class="sxs-lookup"><span data-stu-id="c2cd9-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

