---
title: Migration of managemtn tools resources from Azure Germany to global Azure
description: This article provides help for migrating management tools resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: e91b383f8b87af8b1c4c74728ecf8d9ffd0a003e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866591"
---
# <a name="migration-of-management-tools-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="c181a-103">Migration of management tools resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="c181a-103">Migration of management tools resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="c181a-104">This article will provide you some help for the migration of Azure Management Tool resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-104">This article will provide you some help for the migration of Azure Management Tool resources from Azure Germany to global Azure.</span></span>

## <a name="traffic-manager"></a><span data-ttu-id="c181a-105">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c181a-105">Traffic Manager</span></span>

<span data-ttu-id="c181a-106">Traffic Manager profiles created in Azure Germany can't be migrated to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-106">Traffic Manager profiles created in Azure Germany can't be migrated to global Azure.</span></span> <span data-ttu-id="c181a-107">Since you also migrate all the Traffic Manager endpoints to the target environment, you need to update the Traffic Manager profile anyway.</span><span class="sxs-lookup"><span data-stu-id="c181a-107">Since you also migrate all the Traffic Manager endpoints to the target environment, you need to update the Traffic Manager profile anyway.</span></span>

<span data-ttu-id="c181a-108">Traffic Manager can help you with a smooth migration.</span><span class="sxs-lookup"><span data-stu-id="c181a-108">Traffic Manager can help you with a smooth migration.</span></span> <span data-ttu-id="c181a-109">With Traffic Manager still running in the old environment, you can already define additional endpoints in the target environment.</span><span class="sxs-lookup"><span data-stu-id="c181a-109">With Traffic Manager still running in the old environment, you can already define additional endpoints in the target environment.</span></span> <span data-ttu-id="c181a-110">Once Target Manager runs in the new environment, you can still define endpoints in the old environment that you didn't migrate so far.</span><span class="sxs-lookup"><span data-stu-id="c181a-110">Once Target Manager runs in the new environment, you can still define endpoints in the old environment that you didn't migrate so far.</span></span> <span data-ttu-id="c181a-111">This is known as [the Blue-Green scenario](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="c181a-111">This is known as [the Blue-Green scenario](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/).</span></span> <span data-ttu-id="c181a-112">In short:</span><span class="sxs-lookup"><span data-stu-id="c181a-112">In short:</span></span>

- <span data-ttu-id="c181a-113">Create a new Traffic Manager in Azure global</span><span class="sxs-lookup"><span data-stu-id="c181a-113">Create a new Traffic Manager in Azure global</span></span>
- <span data-ttu-id="c181a-114">Define the endpoints (still in Azure Germany)</span><span class="sxs-lookup"><span data-stu-id="c181a-114">Define the endpoints (still in Azure Germany)</span></span>
- <span data-ttu-id="c181a-115">Change your DNS CNAME to the new Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c181a-115">Change your DNS CNAME to the new Traffic Manager</span></span>
- <span data-ttu-id="c181a-116">Turn off the old Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c181a-116">Turn off the old Traffic Manager</span></span>
- <span data-ttu-id="c181a-117">for each endpoint in Azure Germany:</span><span class="sxs-lookup"><span data-stu-id="c181a-117">for each endpoint in Azure Germany:</span></span>
  - <span data-ttu-id="c181a-118">Migrate the endpoint to global Azure</span><span class="sxs-lookup"><span data-stu-id="c181a-118">Migrate the endpoint to global Azure</span></span>
  - <span data-ttu-id="c181a-119">change the Traffic Manager profile to use the new endpoint</span><span class="sxs-lookup"><span data-stu-id="c181a-119">change the Traffic Manager profile to use the new endpoint</span></span>

### <a name="next-steps"></a><span data-ttu-id="c181a-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="c181a-120">Next steps</span></span>

- <span data-ttu-id="c181a-121">Refresh your knowledge about Traffic Manager by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/traffic-manager/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c181a-121">Refresh your knowledge about Traffic Manager by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/traffic-manager/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="c181a-122">References</span><span class="sxs-lookup"><span data-stu-id="c181a-122">References</span></span>

- [<span data-ttu-id="c181a-123">Traffic Manager overview</span><span class="sxs-lookup"><span data-stu-id="c181a-123">Traffic Manager overview</span></span>](../traffic-manager/traffic-manager-overview.md)
- [<span data-ttu-id="c181a-124">Create a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="c181a-124">Create a Traffic Manager profile</span></span>](../traffic-manager/traffic-manager-create-profile.md)
- [<span data-ttu-id="c181a-125">Blue-Green scenario</span><span class="sxs-lookup"><span data-stu-id="c181a-125">Blue-Green scenario</span></span>](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/)








## <a name="backup"></a><span data-ttu-id="c181a-126">Backup</span><span class="sxs-lookup"><span data-stu-id="c181a-126">Backup</span></span>

<span data-ttu-id="c181a-127">Unfortunately, Azure Backup jobs and snapshots can't be migrated from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-127">Unfortunately, Azure Backup jobs and snapshots can't be migrated from Azure Germany to global Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c181a-128">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c181a-128">Next Steps</span></span>

- <span data-ttu-id="c181a-129">Refresh your knowledge about Azure Backup by following [these Step-by-Step tutorials](https://docs.microsoft.com/azure/backup/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c181a-129">Refresh your knowledge about Azure Backup by following [these Step-by-Step tutorials](https://docs.microsoft.com/azure/backup/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="c181a-130">References</span><span class="sxs-lookup"><span data-stu-id="c181a-130">References</span></span>

- [<span data-ttu-id="c181a-131">Azure Backup overview</span><span class="sxs-lookup"><span data-stu-id="c181a-131">Azure Backup overview</span></span>](../backup/backup-introduction-to-azure-backup.md)










## <a name="scheduler"></a><span data-ttu-id="c181a-132">Scheduler</span><span class="sxs-lookup"><span data-stu-id="c181a-132">Scheduler</span></span>

<span data-ttu-id="c181a-133">Azure Scheduler is being deprecated.</span><span class="sxs-lookup"><span data-stu-id="c181a-133">Azure Scheduler is being deprecated.</span></span> <span data-ttu-id="c181a-134">Use Azure Logic apps instead to create scheduling jobs.</span><span class="sxs-lookup"><span data-stu-id="c181a-134">Use Azure Logic apps instead to create scheduling jobs.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c181a-135">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c181a-135">Next Steps</span></span>

- <span data-ttu-id="c181a-136">Make yourself familiar with the features that [Azure Logic Apps provides by following the [Step-by-Step tutorials](https://docs.microsoft.com/azure/logic-apps/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c181a-136">Make yourself familiar with the features that [Azure Logic Apps provides by following the [Step-by-Step tutorials](https://docs.microsoft.com/azure/logic-apps/#step-by-step-tutorials).</span></span>

### <a name="reference"></a><span data-ttu-id="c181a-137">Reference</span><span class="sxs-lookup"><span data-stu-id="c181a-137">Reference</span></span>

- [<span data-ttu-id="c181a-138">Azure Logic Apps overview</span><span class="sxs-lookup"><span data-stu-id="c181a-138">Azure Logic Apps overview</span></span>](../logic-apps/logic-apps-overview.md)











## <a name="network-watcher"></a><span data-ttu-id="c181a-139">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="c181a-139">Network Watcher</span></span>

<span data-ttu-id="c181a-140">Migration of Network Watcher between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="c181a-140">Migration of Network Watcher between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="c181a-141">The recommended approach is to create and configure a new Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="c181a-141">The recommended approach is to create and configure a new Network Watcher.</span></span> <span data-ttu-id="c181a-142">Afterwards, compare the results between old and new environment:</span><span class="sxs-lookup"><span data-stu-id="c181a-142">Afterwards, compare the results between old and new environment:</span></span>

- [<span data-ttu-id="c181a-143">NSG Flow Logs</span><span class="sxs-lookup"><span data-stu-id="c181a-143">NSG Flow Logs</span></span>](../network-watcher/network-watcher-nsg-flow-logging-portal.md)
- [<span data-ttu-id="c181a-144">Connection Monitor</span><span class="sxs-lookup"><span data-stu-id="c181a-144">Connection Monitor</span></span>](../network-watcher/connection-monitor.md)

### <a name="next-steps"></a><span data-ttu-id="c181a-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="c181a-145">Next steps</span></span>

- <span data-ttu-id="c181a-146">Refresh your knowledge about Network Watcher by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/network-watcher/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c181a-146">Refresh your knowledge about Network Watcher by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/network-watcher/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="c181a-147">References</span><span class="sxs-lookup"><span data-stu-id="c181a-147">References</span></span>

- [<span data-ttu-id="c181a-148">Network Watcher Overview</span><span class="sxs-lookup"><span data-stu-id="c181a-148">Network Watcher Overview</span></span>](../network-watcher/network-watcher-monitoring-overview.md)













## <a name="site-recovery"></a><span data-ttu-id="c181a-149">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c181a-149">Site Recovery</span></span>

<span data-ttu-id="c181a-150">It's not possible to migrate your current Site Recovery setup to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-150">It's not possible to migrate your current Site Recovery setup to global Azure.</span></span> <span data-ttu-id="c181a-151">Set up your solution again in global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-151">Set up your solution again in global Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c181a-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="c181a-152">Next steps</span></span>

<span data-ttu-id="c181a-153">Refresh your knowledge by following these Step-by-Step tutorials for setting up a disaster recovery for</span><span class="sxs-lookup"><span data-stu-id="c181a-153">Refresh your knowledge by following these Step-by-Step tutorials for setting up a disaster recovery for</span></span>
- [<span data-ttu-id="c181a-154">Azure to Azure</span><span class="sxs-lookup"><span data-stu-id="c181a-154">Azure to Azure</span></span>](https://docs.microsoft.com/azure/site-recovery/#azure-to-azure)
- [<span data-ttu-id="c181a-155">Vmware to Azure</span><span class="sxs-lookup"><span data-stu-id="c181a-155">Vmware to Azure</span></span>](https://docs.microsoft.com/azure/site-recovery/#vmware)
- [<span data-ttu-id="c181a-156">Hyper-V to Azure</span><span class="sxs-lookup"><span data-stu-id="c181a-156">Hyper-V to Azure</span></span>](https://docs.microsoft.com/azure/site-recovery/#hyper-v)

### <a name="references"></a><span data-ttu-id="c181a-157">References</span><span class="sxs-lookup"><span data-stu-id="c181a-157">References</span></span>

<span data-ttu-id="c181a-158">See also [how to use Site Recovery](./germany-migration-compute.md#compute-iaas) to migrate VMs from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-158">See also [how to use Site Recovery](./germany-migration-compute.md#compute-iaas) to migrate VMs from Azure Germany to global Azure.</span></span>













## <a name="azure-policy"></a><span data-ttu-id="c181a-159">Azure Policy</span><span class="sxs-lookup"><span data-stu-id="c181a-159">Azure Policy</span></span>

<span data-ttu-id="c181a-160">There's no direct way to migrate policies.</span><span class="sxs-lookup"><span data-stu-id="c181a-160">There's no direct way to migrate policies.</span></span> <span data-ttu-id="c181a-161">The scope of assigned policies will change in the most cases, especially since the subscription ID will change.</span><span class="sxs-lookup"><span data-stu-id="c181a-161">The scope of assigned policies will change in the most cases, especially since the subscription ID will change.</span></span> <span data-ttu-id="c181a-162">But here's a way to preserve policy definitions and reuse them in global Azure.</span><span class="sxs-lookup"><span data-stu-id="c181a-162">But here's a way to preserve policy definitions and reuse them in global Azure.</span></span>

<span data-ttu-id="c181a-163">By using Azure CLI, use this command to list all policies in your current environment.</span><span class="sxs-lookup"><span data-stu-id="c181a-163">By using Azure CLI, use this command to list all policies in your current environment.</span></span>
> [!NOTE]
> <span data-ttu-id="c181a-164">Don't forget to switch to the AzureGermanCloud environment in CLI first.</span><span class="sxs-lookup"><span data-stu-id="c181a-164">Don't forget to switch to the AzureGermanCloud environment in CLI first.</span></span>

```azurecli
az policy definition list --query '[].{Type:policyType,Name:name}' --output table
```

<span data-ttu-id="c181a-165">Only export policies with the PolicyType *Custom*.</span><span class="sxs-lookup"><span data-stu-id="c181a-165">Only export policies with the PolicyType *Custom*.</span></span> <span data-ttu-id="c181a-166">Export the *policyRule* into a file.</span><span class="sxs-lookup"><span data-stu-id="c181a-166">Export the *policyRule* into a file.</span></span> <span data-ttu-id="c181a-167">The following example exports a custom policy "Allow Germany Central Only" (short *allowgconly*) to a file in the current folder.</span><span class="sxs-lookup"><span data-stu-id="c181a-167">The following example exports a custom policy "Allow Germany Central Only" (short *allowgconly*) to a file in the current folder.</span></span> 

```azurecli
az policy definition show --name allowgconly --output json --query policyRule > policy.json
```

<span data-ttu-id="c181a-168">The export file looks something like the following example:</span><span class="sxs-lookup"><span data-stu-id="c181a-168">The export file looks something like the following example:</span></span>

```json
{
  "if": {
    "not": {
      "equals": "germanycentral",
      "field": "location"
    }
  },
  "then": {
    "effect": "Deny"
  }
}
```

<span data-ttu-id="c181a-169">Now switch to the global Azure environment and modify the policy rule by editing the file, for example change *germanycentral* to *westeurope*:</span><span class="sxs-lookup"><span data-stu-id="c181a-169">Now switch to the global Azure environment and modify the policy rule by editing the file, for example change *germanycentral* to *westeurope*:</span></span>

```json
{
  "if": {
    "not": {
      "equals": "westeurope",
      "field": "location"
    }
  },
  "then": {
    "effect": "Deny"
  }
}
```

<span data-ttu-id="c181a-170">Create the new policy:</span><span class="sxs-lookup"><span data-stu-id="c181a-170">Create the new policy:</span></span>

```azurecli
cat policy.json |az policy definition create --name "allowweonly" --rules @-
```

<span data-ttu-id="c181a-171">You now have a new policy named "allowweonly" to allow only West Europe as location.</span><span class="sxs-lookup"><span data-stu-id="c181a-171">You now have a new policy named "allowweonly" to allow only West Europe as location.</span></span>

<span data-ttu-id="c181a-172">Assign the policy to the scopes in your new environment as appropriate.</span><span class="sxs-lookup"><span data-stu-id="c181a-172">Assign the policy to the scopes in your new environment as appropriate.</span></span> <span data-ttu-id="c181a-173">You can document the old assignments in Azure Germany by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c181a-173">You can document the old assignments in Azure Germany by running the following command:</span></span>

```azurecli
az policy assignment list
```

## <a name="next-steps"></a><span data-ttu-id="c181a-174">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c181a-174">Next Steps</span></span>

- <span data-ttu-id="c181a-175">Refresh your knowledge about Azure Policy with [this Step-by-Step tutorial](../azure-policy/create-manage-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c181a-175">Refresh your knowledge about Azure Policy with [this Step-by-Step tutorial](../azure-policy/create-manage-policy.md).</span></span>

## <a name="references"></a><span data-ttu-id="c181a-176">References</span><span class="sxs-lookup"><span data-stu-id="c181a-176">References</span></span>

- [<span data-ttu-id="c181a-177">View policies with CLI</span><span class="sxs-lookup"><span data-stu-id="c181a-177">View policies with CLI</span></span>](../azure-policy/create-manage-policy.md#view-policy-definitions-with-azure-cli)
- [<span data-ttu-id="c181a-178">Create policy definition with CLI</span><span class="sxs-lookup"><span data-stu-id="c181a-178">Create policy definition with CLI</span></span>](../azure-policy/create-manage-policy.md#create-a-policy-definition-with-azure-cli)
- [<span data-ttu-id="c181a-179">View policies with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c181a-179">View policies with PowerShell</span></span>](../azure-policy/create-manage-policy.md#view-policy-definitions-with-powershell)
- [<span data-ttu-id="c181a-180">Create policy definition with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c181a-180">Create policy definition with PowerShell</span></span>](../azure-policy/create-manage-policy.md#create-a-policy-definition-with-powershell)
