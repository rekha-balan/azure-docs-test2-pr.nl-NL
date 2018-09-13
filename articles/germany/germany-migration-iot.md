---
title: Migration of IoT resources from Azure Germany to global Azure
description: This article provides help for migrating IoT resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 1e1f2cc4743fa70aeea4960fd783fda63599f943
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871368"
---
# <a name="migration-of-internet-of-things-iot-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="078ab-103">Migration of Internet of Things (IoT) resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="078ab-103">Migration of Internet of Things (IoT) resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="078ab-104">This article will provide you some help for the migration of Azure IoT resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="078ab-104">This article will provide you some help for the migration of Azure IoT resources from Azure Germany to global Azure.</span></span>

## <a name="azure-cosmos-db"></a><span data-ttu-id="078ab-105">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="078ab-105">Azure Cosmos DB</span></span>

<span data-ttu-id="078ab-106">With the Azure Cosmos DB Data Migration tool, you can easily migrate data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="078ab-106">With the Azure Cosmos DB Data Migration tool, you can easily migrate data to Azure Cosmos DB.</span></span> <span data-ttu-id="078ab-107">The Azure Cosmos DB Data Migration tool is an open-source solution that imports data to Azure Cosmos DB from different sources.</span><span class="sxs-lookup"><span data-stu-id="078ab-107">The Azure Cosmos DB Data Migration tool is an open-source solution that imports data to Azure Cosmos DB from different sources.</span></span>

<span data-ttu-id="078ab-108">The tool is available as a graphical interface tool or as command-line tool.</span><span class="sxs-lookup"><span data-stu-id="078ab-108">The tool is available as a graphical interface tool or as command-line tool.</span></span> <span data-ttu-id="078ab-109">The source code is available in the GitHub repository for [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool), and a compiled version is available on the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=46436).</span><span class="sxs-lookup"><span data-stu-id="078ab-109">The source code is available in the GitHub repository for [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool), and a compiled version is available on the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=46436).</span></span>

<span data-ttu-id="078ab-110">The recommended steps are:</span><span class="sxs-lookup"><span data-stu-id="078ab-110">The recommended steps are:</span></span>

- <span data-ttu-id="078ab-111">Perform a review of application uptime requirements and account configurations to recommend the right action plan.</span><span class="sxs-lookup"><span data-stu-id="078ab-111">Perform a review of application uptime requirements and account configurations to recommend the right action plan.</span></span>
- <span data-ttu-id="078ab-112">Follow the steps to clone the account configurations from Azure Germany to the new region by running the tool</span><span class="sxs-lookup"><span data-stu-id="078ab-112">Follow the steps to clone the account configurations from Azure Germany to the new region by running the tool</span></span>
- <span data-ttu-id="078ab-113">If a maintenance window is possible, follow the steps to copy data from source to destination by running the tool</span><span class="sxs-lookup"><span data-stu-id="078ab-113">If a maintenance window is possible, follow the steps to copy data from source to destination by running the tool</span></span>
- <span data-ttu-id="078ab-114">If a maintenance window isn't possible, follow the steps to copy data from source to destination by running the tool and process that we recommend</span><span class="sxs-lookup"><span data-stu-id="078ab-114">If a maintenance window isn't possible, follow the steps to copy data from source to destination by running the tool and process that we recommend</span></span>
  - <span data-ttu-id="078ab-115">Make changes to read/write in application with config driven approach</span><span class="sxs-lookup"><span data-stu-id="078ab-115">Make changes to read/write in application with config driven approach</span></span>
  - <span data-ttu-id="078ab-116">Perform first-time sync</span><span class="sxs-lookup"><span data-stu-id="078ab-116">Perform first-time sync</span></span>
  - <span data-ttu-id="078ab-117">Setup incremental sync/catch up with change feed</span><span class="sxs-lookup"><span data-stu-id="078ab-117">Setup incremental sync/catch up with change feed</span></span>
  - <span data-ttu-id="078ab-118">Point reads to new account and validate application</span><span class="sxs-lookup"><span data-stu-id="078ab-118">Point reads to new account and validate application</span></span>
  - <span data-ttu-id="078ab-119">Stop writes to old account, validate change feed is caught up, then point writes to new accounts</span><span class="sxs-lookup"><span data-stu-id="078ab-119">Stop writes to old account, validate change feed is caught up, then point writes to new accounts</span></span>
  - <span data-ttu-id="078ab-120">Stop tool, and delete old account</span><span class="sxs-lookup"><span data-stu-id="078ab-120">Stop tool, and delete old account</span></span>
- <span data-ttu-id="078ab-121">Follow the steps to run the tool to validate that data is consistent across the old and new accounts.</span><span class="sxs-lookup"><span data-stu-id="078ab-121">Follow the steps to run the tool to validate that data is consistent across the old and new accounts.</span></span>


### <a name="references"></a><span data-ttu-id="078ab-122">References</span><span class="sxs-lookup"><span data-stu-id="078ab-122">References</span></span>

- [<span data-ttu-id="078ab-123">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="078ab-123">Azure Cosmos DB</span></span>](../cosmos-db/introduction.md)
- [<span data-ttu-id="078ab-124">Import data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="078ab-124">Import data to Azure Cosmos DB</span></span>](../cosmos-db/import-data.md)










## <a name="functions"></a><span data-ttu-id="078ab-125">Functions</span><span class="sxs-lookup"><span data-stu-id="078ab-125">Functions</span></span>

<span data-ttu-id="078ab-126">Migration of Functions between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="078ab-126">Migration of Functions between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="078ab-127">The recommended approach is to export Resource Manager template, change the location, and redeploy to target region.</span><span class="sxs-lookup"><span data-stu-id="078ab-127">The recommended approach is to export Resource Manager template, change the location, and redeploy to target region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="078ab-128">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="078ab-128">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="078ab-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="078ab-129">Next steps</span></span>

- <span data-ttu-id="078ab-130">Refresh your knowledge about Functions by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/azure-functions/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="078ab-130">Refresh your knowledge about Functions by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/azure-functions/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="078ab-131">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="078ab-131">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="078ab-132">References</span><span class="sxs-lookup"><span data-stu-id="078ab-132">References</span></span>

- [<span data-ttu-id="078ab-133">Azure Functions Overview</span><span class="sxs-lookup"><span data-stu-id="078ab-133">Azure Functions Overview</span></span>](../azure-functions/functions-overview.md)
- [<span data-ttu-id="078ab-134">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="078ab-134">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="078ab-135">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="078ab-135">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="078ab-136">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="078ab-136">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
















## <a name="notification-hubs"></a><span data-ttu-id="078ab-137">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="078ab-137">Notification Hubs</span></span>

<span data-ttu-id="078ab-138">To migrate settings from one Notification Hub to another, you can export and import all registration tokens along with tags.</span><span class="sxs-lookup"><span data-stu-id="078ab-138">To migrate settings from one Notification Hub to another, you can export and import all registration tokens along with tags.</span></span> <span data-ttu-id="078ab-139">Here's how:</span><span class="sxs-lookup"><span data-stu-id="078ab-139">Here's how:</span></span>

- <span data-ttu-id="078ab-140">[Export the existing Hub registrations](https://msdn.microsoft.com/library/azure/dn790624.aspx) into an Azure Blob Storage container.</span><span class="sxs-lookup"><span data-stu-id="078ab-140">[Export the existing Hub registrations](https://msdn.microsoft.com/library/azure/dn790624.aspx) into an Azure Blob Storage container.</span></span>
- <span data-ttu-id="078ab-141">Create a new Notification Hub in the target environment</span><span class="sxs-lookup"><span data-stu-id="078ab-141">Create a new Notification Hub in the target environment</span></span>
- <span data-ttu-id="078ab-142">[Import your Registration Tokens](https://msdn.microsoft.com/library/azure/dn790624.aspx) from Azure Blob Storage to your new Hub</span><span class="sxs-lookup"><span data-stu-id="078ab-142">[Import your Registration Tokens](https://msdn.microsoft.com/library/azure/dn790624.aspx) from Azure Blob Storage to your new Hub</span></span>

### <a name="next-steps"></a><span data-ttu-id="078ab-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="078ab-143">Next Steps</span></span>

<span data-ttu-id="078ab-144">Refresh your knowledge about Notification Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/notification-hubs/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="078ab-144">Refresh your knowledge about Notification Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/notification-hubs/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="078ab-145">References</span><span class="sxs-lookup"><span data-stu-id="078ab-145">References</span></span>

- [<span data-ttu-id="078ab-146">Notification Hubs overview</span><span class="sxs-lookup"><span data-stu-id="078ab-146">Notification Hubs overview</span></span>](../notification-hubs/notification-hubs-push-notification-overview.md)








## <a name="iot-hub"></a><span data-ttu-id="078ab-147">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="078ab-147">IoT Hub</span></span>

<span data-ttu-id="078ab-148">A seamless migration of IoT Hub instances from Azure Germany to global Azure isn't possible.</span><span class="sxs-lookup"><span data-stu-id="078ab-148">A seamless migration of IoT Hub instances from Azure Germany to global Azure isn't possible.</span></span> <span data-ttu-id="078ab-149">You can follow these steps to migrate IoT Hub instances from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="078ab-149">You can follow these steps to migrate IoT Hub instances from Azure Germany to global Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="078ab-150">This migration can cause downtime and data loss to your IoT application.</span><span class="sxs-lookup"><span data-stu-id="078ab-150">This migration can cause downtime and data loss to your IoT application.</span></span> <span data-ttu-id="078ab-151">All telemetry messages, C2D commands and Job (schedules and history) related information are not migrated to global Azure.</span><span class="sxs-lookup"><span data-stu-id="078ab-151">All telemetry messages, C2D commands and Job (schedules and history) related information are not migrated to global Azure.</span></span> <span data-ttu-id="078ab-152">You must reconfigure your devices and backend applications to start using the new connection strings.</span><span class="sxs-lookup"><span data-stu-id="078ab-152">You must reconfigure your devices and backend applications to start using the new connection strings.</span></span>

### <a name="step-1---recreate-iot-hub"></a><span data-ttu-id="078ab-153">Step 1 - Recreate IoT Hub</span><span class="sxs-lookup"><span data-stu-id="078ab-153">Step 1 - Recreate IoT Hub</span></span>

<span data-ttu-id="078ab-154">IoT Hub doesn’t support cloning natively.</span><span class="sxs-lookup"><span data-stu-id="078ab-154">IoT Hub doesn’t support cloning natively.</span></span> <span data-ttu-id="078ab-155">However, you can use the Azure Resource Manager feature to [export a resource group as a template](../azure-resource-manager/resource-manager-export-template-powershell.md) to export your IoT hub metadata, including configured routes and other IoT hub settings, and redeploy it in global Azure.</span><span class="sxs-lookup"><span data-stu-id="078ab-155">However, you can use the Azure Resource Manager feature to [export a resource group as a template](../azure-resource-manager/resource-manager-export-template-powershell.md) to export your IoT hub metadata, including configured routes and other IoT hub settings, and redeploy it in global Azure.</span></span> <span data-ttu-id="078ab-156">You may also find it easier to recreate the IoT Hub in the portal by looking at the details in the exported JSON.</span><span class="sxs-lookup"><span data-stu-id="078ab-156">You may also find it easier to recreate the IoT Hub in the portal by looking at the details in the exported JSON.</span></span>

### <a name="step-2---migrate-device-identities"></a><span data-ttu-id="078ab-157">Step 2 - Migrate device identities</span><span class="sxs-lookup"><span data-stu-id="078ab-157">Step 2 - Migrate device identities</span></span>

- <span data-ttu-id="078ab-158">In the source tenant in Azure Germany, use the [ExportDevices](../iot-hub/iot-hub-bulk-identity-mgmt.md) Resource Manager API to export all device identities, device twins, module twins (including the keys) to a storage container.</span><span class="sxs-lookup"><span data-stu-id="078ab-158">In the source tenant in Azure Germany, use the [ExportDevices](../iot-hub/iot-hub-bulk-identity-mgmt.md) Resource Manager API to export all device identities, device twins, module twins (including the keys) to a storage container.</span></span> <span data-ttu-id="078ab-159">You may use a storage container in either Azure Germany or global Azure, just make sure the generated SAS URI has enough permission.</span><span class="sxs-lookup"><span data-stu-id="078ab-159">You may use a storage container in either Azure Germany or global Azure, just make sure the generated SAS URI has enough permission.</span></span> 
- <span data-ttu-id="078ab-160">Run the [ImportDevices](../iot-hub/iot-hub-bulk-identity-mgmt.md) Azure Resource Manager API to import all device identities from the storage container into the cloned IoT hub in global Azure.</span><span class="sxs-lookup"><span data-stu-id="078ab-160">Run the [ImportDevices](../iot-hub/iot-hub-bulk-identity-mgmt.md) Azure Resource Manager API to import all device identities from the storage container into the cloned IoT hub in global Azure.</span></span>
- <span data-ttu-id="078ab-161">Reconfigure your devices and backend services to start using the new connection strings.</span><span class="sxs-lookup"><span data-stu-id="078ab-161">Reconfigure your devices and backend services to start using the new connection strings.</span></span> <span data-ttu-id="078ab-162">The hostname changes from `*.azure-devices.de` to `*.azure-devices.com`.</span><span class="sxs-lookup"><span data-stu-id="078ab-162">The hostname changes from `*.azure-devices.de` to `*.azure-devices.com`.</span></span>  

> [!NOTE]
> <span data-ttu-id="078ab-163">The Root CA is different between the Azure Germany and global Azure, so this needs to be accounted for while reconfiguring your devices and backend applications interacting with the IoT Hub instance.</span><span class="sxs-lookup"><span data-stu-id="078ab-163">The Root CA is different between the Azure Germany and global Azure, so this needs to be accounted for while reconfiguring your devices and backend applications interacting with the IoT Hub instance.</span></span>

### <a name="next-steps"></a><span data-ttu-id="078ab-164">Next Steps</span><span class="sxs-lookup"><span data-stu-id="078ab-164">Next Steps</span></span>

- [<span data-ttu-id="078ab-165">Export IoT Hub bulk identity</span><span class="sxs-lookup"><span data-stu-id="078ab-165">Export IoT Hub bulk identity</span></span>](../iot-hub/iot-hub-bulk-identity-mgmt.md#export-devices)
- [<span data-ttu-id="078ab-166">Import IoT Hub bulk identity</span><span class="sxs-lookup"><span data-stu-id="078ab-166">Import IoT Hub bulk identity</span></span>](../iot-hub/iot-hub-bulk-identity-mgmt.md#import-devices)

### <a name="references"></a><span data-ttu-id="078ab-167">References</span><span class="sxs-lookup"><span data-stu-id="078ab-167">References</span></span>

- [<span data-ttu-id="078ab-168">Azure IoT Hub overview</span><span class="sxs-lookup"><span data-stu-id="078ab-168">Azure IoT Hub overview</span></span>](../iot-hub/about-iot-hub.md)
