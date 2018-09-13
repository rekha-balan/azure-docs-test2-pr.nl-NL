---
title: Migration of compute resources from Azure Germany to global Azure
description: Provides help for migrating compute resources
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: ba2f4575864ef667ca5a77452a1a65aa13345ed5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857695"
---
# <a name="migration-of-compute-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="9f14d-103">Migration of compute resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="9f14d-103">Migration of compute resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="9f14d-104">This article will provide you some help for the migration of Azure Compute resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="9f14d-104">This article will provide you some help for the migration of Azure Compute resources from Azure Germany to global Azure.</span></span>

## <a name="compute-iaas"></a><span data-ttu-id="9f14d-105">Compute IaaS</span><span class="sxs-lookup"><span data-stu-id="9f14d-105">Compute IaaS</span></span>

<span data-ttu-id="9f14d-106">Unfortunately, no direct migration from Azure Germany to global Azure is possible.</span><span class="sxs-lookup"><span data-stu-id="9f14d-106">Unfortunately, no direct migration from Azure Germany to global Azure is possible.</span></span> <span data-ttu-id="9f14d-107">But there's more than one way to "duplicate" your VMs.</span><span class="sxs-lookup"><span data-stu-id="9f14d-107">But there's more than one way to "duplicate" your VMs.</span></span>

### <a name="duplicate-with-azure-site-recovery"></a><span data-ttu-id="9f14d-108">Duplicate with Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9f14d-108">Duplicate with Azure Site Recovery</span></span>

<span data-ttu-id="9f14d-109">Azure Site Recovery can help you migrate your VMs from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="9f14d-109">Azure Site Recovery can help you migrate your VMs from Azure Germany to global Azure.</span></span> <span data-ttu-id="9f14d-110">Since source and target are in different tenants, you can't use the normal Azure Disaster Recovery option available for VMs.</span><span class="sxs-lookup"><span data-stu-id="9f14d-110">Since source and target are in different tenants, you can't use the normal Azure Disaster Recovery option available for VMs.</span></span> <span data-ttu-id="9f14d-111">The trick here is to set up a Site Recovery vault in the target environment (global Azure), and to proceed like moving a physical server into Azure.</span><span class="sxs-lookup"><span data-stu-id="9f14d-111">The trick here is to set up a Site Recovery vault in the target environment (global Azure), and to proceed like moving a physical server into Azure.</span></span> <span data-ttu-id="9f14d-112">Choose a replication path from *not virtualized* to Azure global and - after the replication finished - do a failover.</span><span class="sxs-lookup"><span data-stu-id="9f14d-112">Choose a replication path from *not virtualized* to Azure global and - after the replication finished - do a failover.</span></span>

> [!NOTE]
> <span data-ttu-id="9f14d-113">These steps are the same that you would take to migrate a physical server running on-premise to Azure.</span><span class="sxs-lookup"><span data-stu-id="9f14d-113">These steps are the same that you would take to migrate a physical server running on-premise to Azure.</span></span>

<span data-ttu-id="9f14d-114">There's a [good tutorial for Site Recovery](../site-recovery/physical-azure-disaster-recovery.md) available.</span><span class="sxs-lookup"><span data-stu-id="9f14d-114">There's a [good tutorial for Site Recovery](../site-recovery/physical-azure-disaster-recovery.md) available.</span></span> <span data-ttu-id="9f14d-115">For a quick overview, here's a shorter and slightly adopted version:</span><span class="sxs-lookup"><span data-stu-id="9f14d-115">For a quick overview, here's a shorter and slightly adopted version:</span></span>

<span data-ttu-id="9f14d-116">Install a Configuration/Process Server in your source environment to build the images of the servers.</span><span class="sxs-lookup"><span data-stu-id="9f14d-116">Install a Configuration/Process Server in your source environment to build the images of the servers.</span></span> <span data-ttu-id="9f14d-117">Then replicate the images to the Recovery Service Vault in your target environment.</span><span class="sxs-lookup"><span data-stu-id="9f14d-117">Then replicate the images to the Recovery Service Vault in your target environment.</span></span> <span data-ttu-id="9f14d-118">This is all done by the Configuration Server, and there's no need to touch the single servers.</span><span class="sxs-lookup"><span data-stu-id="9f14d-118">This is all done by the Configuration Server, and there's no need to touch the single servers.</span></span>

- <span data-ttu-id="9f14d-119">Sign in to the Azure Germany Portal</span><span class="sxs-lookup"><span data-stu-id="9f14d-119">Sign in to the Azure Germany Portal</span></span>
- <span data-ttu-id="9f14d-120">Compare the OS version of the VMs you want to migrate against the [support matrix](../site-recovery/vmware-physical-secondary-support-matrix.md)</span><span class="sxs-lookup"><span data-stu-id="9f14d-120">Compare the OS version of the VMs you want to migrate against the [support matrix](../site-recovery/vmware-physical-secondary-support-matrix.md)</span></span>
- <span data-ttu-id="9f14d-121">Set up a new VM in your source VNet acting as the configuration server:</span><span class="sxs-lookup"><span data-stu-id="9f14d-121">Set up a new VM in your source VNet acting as the configuration server:</span></span>
  - <span data-ttu-id="9f14d-122">Choose DS4v3 or higher (4-8 cores, 16 GB Memory)</span><span class="sxs-lookup"><span data-stu-id="9f14d-122">Choose DS4v3 or higher (4-8 cores, 16 GB Memory)</span></span>
  - <span data-ttu-id="9f14d-123">Attach an additional disk with at least 1 TB available space (for the VM images)</span><span class="sxs-lookup"><span data-stu-id="9f14d-123">Attach an additional disk with at least 1 TB available space (for the VM images)</span></span>
  - <span data-ttu-id="9f14d-124">Use Windows Server 2012R2 or higher</span><span class="sxs-lookup"><span data-stu-id="9f14d-124">Use Windows Server 2012R2 or higher</span></span>
- <span data-ttu-id="9f14d-125">Make sure ports 443 and 9443 are open for the subnet in both directions</span><span class="sxs-lookup"><span data-stu-id="9f14d-125">Make sure ports 443 and 9443 are open for the subnet in both directions</span></span>
- <span data-ttu-id="9f14d-126">Sign in to this new VM (ConfigurationServer)</span><span class="sxs-lookup"><span data-stu-id="9f14d-126">Sign in to this new VM (ConfigurationServer)</span></span>
- <span data-ttu-id="9f14d-127">From within your remote desktop session, sign in to the global Azure portal with your global Azure credentials</span><span class="sxs-lookup"><span data-stu-id="9f14d-127">From within your remote desktop session, sign in to the global Azure portal with your global Azure credentials</span></span>
- <span data-ttu-id="9f14d-128">Set up a VNet where the replicated VMs will run</span><span class="sxs-lookup"><span data-stu-id="9f14d-128">Set up a VNet where the replicated VMs will run</span></span>
- <span data-ttu-id="9f14d-129">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="9f14d-129">Create a storage account</span></span>
- <span data-ttu-id="9f14d-130">Set up the Recovery Service Vault</span><span class="sxs-lookup"><span data-stu-id="9f14d-130">Set up the Recovery Service Vault</span></span>
- <span data-ttu-id="9f14d-131">Define Protection goal (**To Azure** -- **Not virtualized/other**)</span><span class="sxs-lookup"><span data-stu-id="9f14d-131">Define Protection goal (**To Azure** -- **Not virtualized/other**)</span></span>
- <span data-ttu-id="9f14d-132">Download Recovery Unified Setup installation file (**Prepare Infrastructure** > **Source**).</span><span class="sxs-lookup"><span data-stu-id="9f14d-132">Download Recovery Unified Setup installation file (**Prepare Infrastructure** > **Source**).</span></span> <span data-ttu-id="9f14d-133">When you opened the portal URL from within the ConfigurationServer, the file will be downloaded to the correct server.</span><span class="sxs-lookup"><span data-stu-id="9f14d-133">When you opened the portal URL from within the ConfigurationServer, the file will be downloaded to the correct server.</span></span> <span data-ttu-id="9f14d-134">If not, upload the install file to the ConfigurationServer.</span><span class="sxs-lookup"><span data-stu-id="9f14d-134">If not, upload the install file to the ConfigurationServer.</span></span>
- <span data-ttu-id="9f14d-135">Download the vault registration key (and upload to ConfigurationServer like above if necessary)</span><span class="sxs-lookup"><span data-stu-id="9f14d-135">Download the vault registration key (and upload to ConfigurationServer like above if necessary)</span></span>
- <span data-ttu-id="9f14d-136">Run the Recovery Unified Setup installation on the ConfigurationServer</span><span class="sxs-lookup"><span data-stu-id="9f14d-136">Run the Recovery Unified Setup installation on the ConfigurationServer</span></span>
- <span data-ttu-id="9f14d-137">Set up the target environment (you should still be signed in to the target portal)</span><span class="sxs-lookup"><span data-stu-id="9f14d-137">Set up the target environment (you should still be signed in to the target portal)</span></span>
- <span data-ttu-id="9f14d-138">Define replication policy</span><span class="sxs-lookup"><span data-stu-id="9f14d-138">Define replication policy</span></span>
- <span data-ttu-id="9f14d-139">Start replication</span><span class="sxs-lookup"><span data-stu-id="9f14d-139">Start replication</span></span>

<span data-ttu-id="9f14d-140">When replication has succeeded the first time, you should test the scenario by doing a test failover, verifying and deleting the test.</span><span class="sxs-lookup"><span data-stu-id="9f14d-140">When replication has succeeded the first time, you should test the scenario by doing a test failover, verifying and deleting the test.</span></span> <span data-ttu-id="9f14d-141">Your final step is to do the real failover.</span><span class="sxs-lookup"><span data-stu-id="9f14d-141">Your final step is to do the real failover.</span></span>

> [!CAUTION]
> <span data-ttu-id="9f14d-142">There is no synchronization back to the source VM.</span><span class="sxs-lookup"><span data-stu-id="9f14d-142">There is no synchronization back to the source VM.</span></span> <span data-ttu-id="9f14d-143">If you want to re-migrate, you must clean up everything and start again at the beginning!</span><span class="sxs-lookup"><span data-stu-id="9f14d-143">If you want to re-migrate, you must clean up everything and start again at the beginning!</span></span>

### <a name="duplicate-with-resource-manager-template-exportimport"></a><span data-ttu-id="9f14d-144">Duplicate with Resource Manager template export/import</span><span class="sxs-lookup"><span data-stu-id="9f14d-144">Duplicate with Resource Manager template export/import</span></span>

<span data-ttu-id="9f14d-145">You can export the Resource Manager template used for the deployment to your local machine.</span><span class="sxs-lookup"><span data-stu-id="9f14d-145">You can export the Resource Manager template used for the deployment to your local machine.</span></span> <span data-ttu-id="9f14d-146">Edit the template to change location and other parameters or variables, and then redeploy in Azure global.</span><span class="sxs-lookup"><span data-stu-id="9f14d-146">Edit the template to change location and other parameters or variables, and then redeploy in Azure global.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9f14d-147">Change Location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-147">Change Location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

<span data-ttu-id="9f14d-148">Export the Resource Manager template in the portal by selecting the resource group.</span><span class="sxs-lookup"><span data-stu-id="9f14d-148">Export the Resource Manager template in the portal by selecting the resource group.</span></span> <span data-ttu-id="9f14d-149">Click *deployments* and select the most recent deployment.</span><span class="sxs-lookup"><span data-stu-id="9f14d-149">Click *deployments* and select the most recent deployment.</span></span> <span data-ttu-id="9f14d-150">Click *Template* in the left menu and download it.</span><span class="sxs-lookup"><span data-stu-id="9f14d-150">Click *Template* in the left menu and download it.</span></span>

<span data-ttu-id="9f14d-151">You get a zip file with several files in it.</span><span class="sxs-lookup"><span data-stu-id="9f14d-151">You get a zip file with several files in it.</span></span> <span data-ttu-id="9f14d-152">The PowerShell, CLI, Ruby, or .NET scripts help you to deploy your template.</span><span class="sxs-lookup"><span data-stu-id="9f14d-152">The PowerShell, CLI, Ruby, or .NET scripts help you to deploy your template.</span></span> <span data-ttu-id="9f14d-153">The file *parameters.json* has all the input from the last deployment, most likely you have to change some settings here.</span><span class="sxs-lookup"><span data-stu-id="9f14d-153">The file *parameters.json* has all the input from the last deployment, most likely you have to change some settings here.</span></span> <span data-ttu-id="9f14d-154">Edit the *template.json* file if you only want to redeploy a subset of the resources.</span><span class="sxs-lookup"><span data-stu-id="9f14d-154">Edit the *template.json* file if you only want to redeploy a subset of the resources.</span></span>


### <a name="next-steps"></a><span data-ttu-id="9f14d-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-155">Next steps</span></span>

- <span data-ttu-id="9f14d-156">Refresh your knowledge about Azure Site Recovery by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/site-recovery/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-156">Refresh your knowledge about Azure Site Recovery by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/site-recovery/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="9f14d-157">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f14d-157">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="reference"></a><span data-ttu-id="9f14d-158">Reference</span><span class="sxs-lookup"><span data-stu-id="9f14d-158">Reference</span></span>

- [<span data-ttu-id="9f14d-159">Physical to Azure using Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9f14d-159">Physical to Azure using Site Recovery</span></span>](../site-recovery/physical-azure-disaster-recovery.md)
- [<span data-ttu-id="9f14d-160">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f14d-160">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="9f14d-161">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="9f14d-161">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="9f14d-162">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="9f14d-162">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)







## <a name="cloud-services"></a><span data-ttu-id="9f14d-163">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="9f14d-163">Cloud Services</span></span>

<span data-ttu-id="9f14d-164">Cloud Services can be redeployed by providing the `.cspkg` and `.cscfg` definitions again.</span><span class="sxs-lookup"><span data-stu-id="9f14d-164">Cloud Services can be redeployed by providing the `.cspkg` and `.cscfg` definitions again.</span></span>

### <a name="by-portal"></a><span data-ttu-id="9f14d-165">By portal</span><span class="sxs-lookup"><span data-stu-id="9f14d-165">By portal</span></span>

- <span data-ttu-id="9f14d-166">[Create a new Cloud Service](../cloud-services/cloud-services-how-to-create-deploy-portal.md) with your `.cspkg` and `.cscfg`.</span><span class="sxs-lookup"><span data-stu-id="9f14d-166">[Create a new Cloud Service](../cloud-services/cloud-services-how-to-create-deploy-portal.md) with your `.cspkg` and `.cscfg`.</span></span>
- <span data-ttu-id="9f14d-167">Update the [CNAME or A record](../cloud-services/cloud-services-custom-domain-name-portal.md) to point traffic to the new cloud service.</span><span class="sxs-lookup"><span data-stu-id="9f14d-167">Update the [CNAME or A record](../cloud-services/cloud-services-custom-domain-name-portal.md) to point traffic to the new cloud service.</span></span>
- <span data-ttu-id="9f14d-168">Delete your old cloud service in Azure Germany after your traffic is pointing to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="9f14d-168">Delete your old cloud service in Azure Germany after your traffic is pointing to the new Cloud Service.</span></span>

### <a name="by-powershell"></a><span data-ttu-id="9f14d-169">By PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f14d-169">By PowerShell</span></span>

- <span data-ttu-id="9f14d-170">[Create a new Cloud Service](/powershell/module/azure/new-azureservice?view=azuresmps-4.0.0) with your `.cspkg` and `.cscfg`.</span><span class="sxs-lookup"><span data-stu-id="9f14d-170">[Create a new Cloud Service](/powershell/module/azure/new-azureservice?view=azuresmps-4.0.0) with your `.cspkg` and `.cscfg`.</span></span>

```powershell
New-AzureService -ServiceName <yourServiceName> -Label <MyTestService> -Location <westeurope>
```

- <span data-ttu-id="9f14d-171">[Create a new deployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-4.0.0) with your `.cspkg` and `.cscfg`.</span><span class="sxs-lookup"><span data-stu-id="9f14d-171">[Create a new deployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-4.0.0) with your `.cspkg` and `.cscfg`.</span></span> <span data-ttu-id="9f14d-172">See details [here].</span><span class="sxs-lookup"><span data-stu-id="9f14d-172">See details [here].</span></span>

```powershell
New-AzureDeployment -ServiceName <yourServiceName> -Slot <Production> -Package <YourCspkgFile.cspkg> -Configuration <YourConfigFile.cscfg>
```

- <span data-ttu-id="9f14d-173">Update the [CNAME or A record](../cloud-services/cloud-services-custom-domain-name-portal.md) to point traffic to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="9f14d-173">Update the [CNAME or A record](../cloud-services/cloud-services-custom-domain-name-portal.md) to point traffic to the new Cloud Service.</span></span>
- <span data-ttu-id="9f14d-174">[Delete your old Cloud Service](/powershell/module/azure/remove-azureservice?view=azuresmps-4.0.0) in Azure Germany after your traffic is pointing to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="9f14d-174">[Delete your old Cloud Service](/powershell/module/azure/remove-azureservice?view=azuresmps-4.0.0) in Azure Germany after your traffic is pointing to the new Cloud Service.</span></span>

```powershell
Remove-AzureService -ServiceName <yourOldServiceName>
```

### <a name="by-rest-api"></a><span data-ttu-id="9f14d-175">By REST API</span><span class="sxs-lookup"><span data-stu-id="9f14d-175">By REST API</span></span>

- <span data-ttu-id="9f14d-176">[Create a new cloud service](/rest/api/compute/cloudservices/rest-create-cloud-service) in the target environment.</span><span class="sxs-lookup"><span data-stu-id="9f14d-176">[Create a new cloud service](/rest/api/compute/cloudservices/rest-create-cloud-service) in the target environment.</span></span>

```http
https://management.core.windows.net/<subscription-id>/services/hostedservices
```

- <span data-ttu-id="9f14d-177">Create a new deployment by using the [create deployment API](https://msdn.microsoft.com/library/azure/ee460813.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f14d-177">Create a new deployment by using the [create deployment API](https://msdn.microsoft.com/library/azure/ee460813.aspx).</span></span> <span data-ttu-id="9f14d-178">If you need to find your `.cspkg` and `.cscfg`, you can call the [Get-Package API](https://msdn.microsoft.com/library/azure/jj154121.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f14d-178">If you need to find your `.cspkg` and `.cscfg`, you can call the [Get-Package API](https://msdn.microsoft.com/library/azure/jj154121.aspx).</span></span>

```http
https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deploymentslots/production
```

- <span data-ttu-id="9f14d-179">[Delete your old Cloud Service](https://docs.microsoft.com/rest/api/compute/cloudservices/rest-delete-cloud-service) in Azure Germany after your traffic is pointing to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="9f14d-179">[Delete your old Cloud Service](https://docs.microsoft.com/rest/api/compute/cloudservices/rest-delete-cloud-service) in Azure Germany after your traffic is pointing to the new Cloud Service.</span></span>

```http
https://management.core.cloudapi.de/<subscription-id>/services/hostedservices/<old-cloudservice-name>
```

### <a name="references"></a><span data-ttu-id="9f14d-180">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-180">References</span></span>
- [<span data-ttu-id="9f14d-181">Cloud Services Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-181">Cloud Services Overview</span></span>](../cloud-services/cloud-services-choose-me.md)











## <a name="service-fabric"></a><span data-ttu-id="9f14d-182">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9f14d-182">Service Fabric</span></span>

<span data-ttu-id="9f14d-183">It's not possible to migrate Service Fabric resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="9f14d-183">It's not possible to migrate Service Fabric resources from Azure Germany to global Azure.</span></span> <span data-ttu-id="9f14d-184">You must re-deploy in the new environment.</span><span class="sxs-lookup"><span data-stu-id="9f14d-184">You must re-deploy in the new environment.</span></span>

<span data-ttu-id="9f14d-185">You can gather some information about your current service fabric environment by using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9f14d-185">You can gather some information about your current service fabric environment by using PowerShell cmdlets.</span></span> <span data-ttu-id="9f14d-186">You find all cmdlets related to service fabric by entering `Get-Help *ServiceFabric*` in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f14d-186">You find all cmdlets related to service fabric by entering `Get-Help *ServiceFabric*` in PowerShell.</span></span>

 
### <a name="next-steps"></a><span data-ttu-id="9f14d-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-187">Next steps</span></span>

- <span data-ttu-id="9f14d-188">Refresh your knowledge about Service Fabric by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/service-fabric/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-188">Refresh your knowledge about Service Fabric by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/service-fabric/#step-by-step-tutorials).</span></span>
- [<span data-ttu-id="9f14d-189">Create a new cluster</span><span class="sxs-lookup"><span data-stu-id="9f14d-189">Create a new cluster</span></span>](../service-fabric/service-fabric-cluster-creation-via-portal.md)

### <a name="references"></a><span data-ttu-id="9f14d-190">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-190">References</span></span>

- [<span data-ttu-id="9f14d-191">Service Fabric Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-191">Service Fabric Overview</span></span>](../service-fabric/service-fabric-overview.md)












## <a name="batch"></a><span data-ttu-id="9f14d-192">Batch</span><span class="sxs-lookup"><span data-stu-id="9f14d-192">Batch</span></span>

<span data-ttu-id="9f14d-193">It's not possible to migrate Batch account data from one region to another.</span><span class="sxs-lookup"><span data-stu-id="9f14d-193">It's not possible to migrate Batch account data from one region to another.</span></span> <span data-ttu-id="9f14d-194">The account may have running VMs associated with it, interacting with data in storage accounts, databases, or other storage systems.</span><span class="sxs-lookup"><span data-stu-id="9f14d-194">The account may have running VMs associated with it, interacting with data in storage accounts, databases, or other storage systems.</span></span>

<span data-ttu-id="9f14d-195">Redeploy your deployment scripts, templates, or code in the new region, including:</span><span class="sxs-lookup"><span data-stu-id="9f14d-195">Redeploy your deployment scripts, templates, or code in the new region, including:</span></span>

- [<span data-ttu-id="9f14d-196">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="9f14d-196">Create a Batch account</span></span>](../batch/batch-account-create-portal.md)
- [<span data-ttu-id="9f14d-197">Get Batch account quota increased</span><span class="sxs-lookup"><span data-stu-id="9f14d-197">Get Batch account quota increased</span></span>](../batch/batch-quota-limit.md)
- <span data-ttu-id="9f14d-198">Create Batch pools</span><span class="sxs-lookup"><span data-stu-id="9f14d-198">Create Batch pools</span></span>
- <span data-ttu-id="9f14d-199">Create new storage accounts, databases, or whatever services used to persist input and output data.</span><span class="sxs-lookup"><span data-stu-id="9f14d-199">Create new storage accounts, databases, or whatever services used to persist input and output data.</span></span>
- <span data-ttu-id="9f14d-200">Update configuration and code to point to new Batch account and use new credentials.</span><span class="sxs-lookup"><span data-stu-id="9f14d-200">Update configuration and code to point to new Batch account and use new credentials.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9f14d-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-201">Next steps</span></span>

- <span data-ttu-id="9f14d-202">Refresh your knowledge about Azure Batch by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/batch/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-202">Refresh your knowledge about Azure Batch by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/batch/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="9f14d-203">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-203">References</span></span>

- [<span data-ttu-id="9f14d-204">Azure Batch Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-204">Azure Batch Overview</span></span>](../batch/batch-technical-overview.md)










## <a name="functions"></a><span data-ttu-id="9f14d-205">Functions</span><span class="sxs-lookup"><span data-stu-id="9f14d-205">Functions</span></span>

<span data-ttu-id="9f14d-206">Migration of Functions between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="9f14d-206">Migration of Functions between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="9f14d-207">The recommended approach is to export Resource Manager template, change the location, and redeploy to target region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-207">The recommended approach is to export Resource Manager template, change the location, and redeploy to target region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f14d-208">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-208">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9f14d-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-209">Next steps</span></span>

- <span data-ttu-id="9f14d-210">Refresh your knowledge about Functions by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/azure-functions/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-210">Refresh your knowledge about Functions by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/azure-functions/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="9f14d-211">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f14d-211">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="9f14d-212">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-212">References</span></span>

- [<span data-ttu-id="9f14d-213">Azure Functions Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-213">Azure Functions Overview</span></span>](../azure-functions/functions-overview.md)
- [<span data-ttu-id="9f14d-214">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f14d-214">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="9f14d-215">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="9f14d-215">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="9f14d-216">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="9f14d-216">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)











## <a name="virtual-machines-scale-set"></a><span data-ttu-id="9f14d-217">Virtual Machines Scale Set</span><span class="sxs-lookup"><span data-stu-id="9f14d-217">Virtual Machines Scale Set</span></span>

<span data-ttu-id="9f14d-218">The recommended approach is to export the Resource Manager template, adopt it to the new environment, and redeploy it to target region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-218">The recommended approach is to export the Resource Manager template, adopt it to the new environment, and redeploy it to target region.</span></span> <span data-ttu-id="9f14d-219">You should just export the base template and redeploy it in the new environment, as individual VMSS instances should all be the same.</span><span class="sxs-lookup"><span data-stu-id="9f14d-219">You should just export the base template and redeploy it in the new environment, as individual VMSS instances should all be the same.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f14d-220">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-220">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9f14d-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-221">Next steps</span></span>

- <span data-ttu-id="9f14d-222">Refresh your knowledge about Virtual Machine Scale Sets following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/virtual-machine-scale-sets/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-222">Refresh your knowledge about Virtual Machine Scale Sets following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/virtual-machine-scale-sets/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="9f14d-223">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md)</span><span class="sxs-lookup"><span data-stu-id="9f14d-223">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md)</span></span>
- <span data-ttu-id="9f14d-224">Read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f14d-224">Read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="9f14d-225">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-225">References</span></span>

- [<span data-ttu-id="9f14d-226">Azure Virtual Machine Scale Set Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-226">Azure Virtual Machine Scale Set Overview</span></span>](../virtual-machine-scale-sets/overview.md)
- [<span data-ttu-id="9f14d-227">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f14d-227">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="9f14d-228">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="9f14d-228">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="9f14d-229">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="9f14d-229">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)










## <a name="app-service---web-apps"></a><span data-ttu-id="9f14d-230">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="9f14d-230">App Service - Web Apps</span></span>

<span data-ttu-id="9f14d-231">The migration of App Services from Azure Germany to global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="9f14d-231">The migration of App Services from Azure Germany to global Azure isn't supported at this time.</span></span> <span data-ttu-id="9f14d-232">The recommended approach is to export as Resource Manager template and redeploy after changing the location property to the new destination region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-232">The recommended approach is to export as Resource Manager template and redeploy after changing the location property to the new destination region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f14d-233">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="9f14d-233">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9f14d-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f14d-234">Next steps</span></span>

- <span data-ttu-id="9f14d-235">Refresh your knowledge about App Services by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/app-service/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="9f14d-235">Refresh your knowledge about App Services by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/app-service/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="9f14d-236">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f14d-236">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="9f14d-237">References</span><span class="sxs-lookup"><span data-stu-id="9f14d-237">References</span></span>

- [<span data-ttu-id="9f14d-238">App Service Overview</span><span class="sxs-lookup"><span data-stu-id="9f14d-238">App Service Overview</span></span>](../app-service/app-service-web-overview.md)
- [<span data-ttu-id="9f14d-239">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f14d-239">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="9f14d-240">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="9f14d-240">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="9f14d-241">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="9f14d-241">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
