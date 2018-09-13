---
title: Cloud Services Role config XPath cheat sheet | Microsoft Docs
description: The various XPath settings you can use in the cloud service role config to expose settings as an environment variable.
services: cloud-services
documentationcenter: ''
author: jpconnock
manager: timlt
editor: ''
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: jeconnoc
ms.openlocfilehash: 2db63be6c6997840f7409a3ca79f1845f30e4ceb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829452"
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="7ba56-103">Expose role configuration settings as an environment variable with XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="7ba56-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span><span class="sxs-lookup"><span data-stu-id="7ba56-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="7ba56-105">The following XPath values are supported (which correspond to API values).</span><span class="sxs-lookup"><span data-stu-id="7ba56-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="7ba56-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span><span class="sxs-lookup"><span data-stu-id="7ba56-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="7ba56-107">App running in emulator</span><span class="sxs-lookup"><span data-stu-id="7ba56-107">App running in emulator</span></span>
<span data-ttu-id="7ba56-108">Indicates that the app is running in the emulator.</span><span class="sxs-lookup"><span data-stu-id="7ba56-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="7ba56-109">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-109">Type</span></span> | <span data-ttu-id="7ba56-110">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-111">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-111">XPath</span></span> |<span data-ttu-id="7ba56-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="7ba56-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="7ba56-113">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-113">Code</span></span> |<span data-ttu-id="7ba56-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="7ba56-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="7ba56-115">Deployment ID</span><span class="sxs-lookup"><span data-stu-id="7ba56-115">Deployment ID</span></span>
<span data-ttu-id="7ba56-116">Retrieves the deployment ID for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="7ba56-117">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-117">Type</span></span> | <span data-ttu-id="7ba56-118">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-119">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-119">XPath</span></span> |<span data-ttu-id="7ba56-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="7ba56-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="7ba56-121">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-121">Code</span></span> |<span data-ttu-id="7ba56-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="7ba56-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="7ba56-123">Role ID</span><span class="sxs-lookup"><span data-stu-id="7ba56-123">Role ID</span></span>
<span data-ttu-id="7ba56-124">Retrieves the current role ID for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="7ba56-125">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-125">Type</span></span> | <span data-ttu-id="7ba56-126">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-127">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-127">XPath</span></span> |<span data-ttu-id="7ba56-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="7ba56-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="7ba56-129">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-129">Code</span></span> |<span data-ttu-id="7ba56-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="7ba56-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="7ba56-131">Update domain</span><span class="sxs-lookup"><span data-stu-id="7ba56-131">Update domain</span></span>
<span data-ttu-id="7ba56-132">Retrieves the update domain of the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="7ba56-133">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-133">Type</span></span> | <span data-ttu-id="7ba56-134">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-135">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-135">XPath</span></span> |<span data-ttu-id="7ba56-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="7ba56-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="7ba56-137">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-137">Code</span></span> |<span data-ttu-id="7ba56-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="7ba56-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="7ba56-139">Fault domain</span><span class="sxs-lookup"><span data-stu-id="7ba56-139">Fault domain</span></span>
<span data-ttu-id="7ba56-140">Retrieves the fault domain of the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="7ba56-141">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-141">Type</span></span> | <span data-ttu-id="7ba56-142">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-143">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-143">XPath</span></span> |<span data-ttu-id="7ba56-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="7ba56-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="7ba56-145">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-145">Code</span></span> |<span data-ttu-id="7ba56-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="7ba56-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="7ba56-147">Role name</span><span class="sxs-lookup"><span data-stu-id="7ba56-147">Role name</span></span>
<span data-ttu-id="7ba56-148">Retrieves the role name of the instances.</span><span class="sxs-lookup"><span data-stu-id="7ba56-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="7ba56-149">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-149">Type</span></span> | <span data-ttu-id="7ba56-150">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-151">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-151">XPath</span></span> |<span data-ttu-id="7ba56-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="7ba56-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="7ba56-153">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-153">Code</span></span> |<span data-ttu-id="7ba56-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="7ba56-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="7ba56-155">Config setting</span><span class="sxs-lookup"><span data-stu-id="7ba56-155">Config setting</span></span>
<span data-ttu-id="7ba56-156">Retrieves the value of the specified configuration setting.</span><span class="sxs-lookup"><span data-stu-id="7ba56-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="7ba56-157">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-157">Type</span></span> | <span data-ttu-id="7ba56-158">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-159">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-159">XPath</span></span> |<span data-ttu-id="7ba56-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="7ba56-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="7ba56-161">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-161">Code</span></span> |<span data-ttu-id="7ba56-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="7ba56-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="7ba56-163">Local storage path</span><span class="sxs-lookup"><span data-stu-id="7ba56-163">Local storage path</span></span>
<span data-ttu-id="7ba56-164">Retrieves the local storage path for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="7ba56-165">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-165">Type</span></span> | <span data-ttu-id="7ba56-166">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-167">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-167">XPath</span></span> |<span data-ttu-id="7ba56-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="7ba56-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="7ba56-169">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-169">Code</span></span> |<span data-ttu-id="7ba56-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="7ba56-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="7ba56-171">Local storage size</span><span class="sxs-lookup"><span data-stu-id="7ba56-171">Local storage size</span></span>
<span data-ttu-id="7ba56-172">Retrieves the size of the local storage for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="7ba56-173">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-173">Type</span></span> | <span data-ttu-id="7ba56-174">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-175">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-175">XPath</span></span> |<span data-ttu-id="7ba56-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="7ba56-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="7ba56-177">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-177">Code</span></span> |<span data-ttu-id="7ba56-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="7ba56-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="7ba56-179">Endpoint protocol</span><span class="sxs-lookup"><span data-stu-id="7ba56-179">Endpoint protocol</span></span>
<span data-ttu-id="7ba56-180">Retrieves the endpoint protocol for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="7ba56-181">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-181">Type</span></span> | <span data-ttu-id="7ba56-182">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-183">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-183">XPath</span></span> |<span data-ttu-id="7ba56-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="7ba56-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="7ba56-185">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-185">Code</span></span> |<span data-ttu-id="7ba56-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="7ba56-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="7ba56-187">Endpoint IP</span><span class="sxs-lookup"><span data-stu-id="7ba56-187">Endpoint IP</span></span>
<span data-ttu-id="7ba56-188">Gets the specified endpoint's IP address.</span><span class="sxs-lookup"><span data-stu-id="7ba56-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="7ba56-189">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-189">Type</span></span> | <span data-ttu-id="7ba56-190">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-191">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-191">XPath</span></span> |<span data-ttu-id="7ba56-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="7ba56-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="7ba56-193">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-193">Code</span></span> |<span data-ttu-id="7ba56-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="7ba56-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="7ba56-195">Endpoint port</span><span class="sxs-lookup"><span data-stu-id="7ba56-195">Endpoint port</span></span>
<span data-ttu-id="7ba56-196">Retrieves the endpoint port for the instance.</span><span class="sxs-lookup"><span data-stu-id="7ba56-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="7ba56-197">Type</span><span class="sxs-lookup"><span data-stu-id="7ba56-197">Type</span></span> | <span data-ttu-id="7ba56-198">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="7ba56-199">XPath</span><span class="sxs-lookup"><span data-stu-id="7ba56-199">XPath</span></span> |<span data-ttu-id="7ba56-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="7ba56-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="7ba56-201">Code</span><span class="sxs-lookup"><span data-stu-id="7ba56-201">Code</span></span> |<span data-ttu-id="7ba56-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="7ba56-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="7ba56-203">Example</span><span class="sxs-lookup"><span data-stu-id="7ba56-203">Example</span></span>
<span data-ttu-id="7ba56-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="7ba56-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="7ba56-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ba56-205">Next steps</span></span>
<span data-ttu-id="7ba56-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span><span class="sxs-lookup"><span data-stu-id="7ba56-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="7ba56-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span><span class="sxs-lookup"><span data-stu-id="7ba56-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="7ba56-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop-new-portal.md) for a role.</span><span class="sxs-lookup"><span data-stu-id="7ba56-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop-new-portal.md) for a role.</span></span>

