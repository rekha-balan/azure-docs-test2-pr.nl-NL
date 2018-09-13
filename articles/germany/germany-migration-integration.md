---
title: Migration of integration resources from Azure Germany to global Azure
description: This article provides help for migrating integration resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 16e7ffa822f645c2a5a070ab3c693cef84a1a85c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871422"
---
# <a name="migration-of-integration-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="4863f-103">Migration of integration resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="4863f-103">Migration of integration resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="4863f-104">This article will provide you some help for the migration of Azure Integration resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="4863f-104">This article will provide you some help for the migration of Azure Integration resources from Azure Germany to global Azure.</span></span>

## <a name="service-bus"></a><span data-ttu-id="4863f-105">Service Bus</span><span class="sxs-lookup"><span data-stu-id="4863f-105">Service Bus</span></span>

<span data-ttu-id="4863f-106">Service Bus services don't have data export or import capabilities.</span><span class="sxs-lookup"><span data-stu-id="4863f-106">Service Bus services don't have data export or import capabilities.</span></span> <span data-ttu-id="4863f-107">To migrate Service Bus from Azure Germany to global Azure, you can export the Service Bus resources [as a Resource Manager template](../azure-resource-manager/resource-manager-export-template-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4863f-107">To migrate Service Bus from Azure Germany to global Azure, you can export the Service Bus resources [as a Resource Manager template](../azure-resource-manager/resource-manager-export-template-powershell.md).</span></span> <span data-ttu-id="4863f-108">Then adopt the exported template for global Azure and recreate the resources.</span><span class="sxs-lookup"><span data-stu-id="4863f-108">Then adopt the exported template for global Azure and recreate the resources.</span></span>

> [!NOTE]
> <span data-ttu-id="4863f-109">This doesn't copy the data (for example messages), it's only recreating the metadata.</span><span class="sxs-lookup"><span data-stu-id="4863f-109">This doesn't copy the data (for example messages), it's only recreating the metadata.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4863f-110">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="4863f-110">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="metadata-service-bus"></a><span data-ttu-id="4863f-111">Metadata Service Bus</span><span class="sxs-lookup"><span data-stu-id="4863f-111">Metadata Service Bus</span></span>

- <span data-ttu-id="4863f-112">Namespaces</span><span class="sxs-lookup"><span data-stu-id="4863f-112">Namespaces</span></span>
- <span data-ttu-id="4863f-113">Queues</span><span class="sxs-lookup"><span data-stu-id="4863f-113">Queues</span></span>
- <span data-ttu-id="4863f-114">Topics</span><span class="sxs-lookup"><span data-stu-id="4863f-114">Topics</span></span>
- <span data-ttu-id="4863f-115">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="4863f-115">Subscriptions</span></span>
- <span data-ttu-id="4863f-116">Rules</span><span class="sxs-lookup"><span data-stu-id="4863f-116">Rules</span></span>
- <span data-ttu-id="4863f-117">AuthorizationRules (see also below)</span><span class="sxs-lookup"><span data-stu-id="4863f-117">AuthorizationRules (see also below)</span></span>

### <a name="keys"></a><span data-ttu-id="4863f-118">Keys</span><span class="sxs-lookup"><span data-stu-id="4863f-118">Keys</span></span>

<span data-ttu-id="4863f-119">The Export/Recreate steps above won't copy the SAS keys associated with Authorization rules.</span><span class="sxs-lookup"><span data-stu-id="4863f-119">The Export/Recreate steps above won't copy the SAS keys associated with Authorization rules.</span></span> <span data-ttu-id="4863f-120">If you need to preserve the SAS keys, use the `New-AzureRmServiceBuskey` cmdlet with the optional parameter `-Keyvalue` to accept the key as string.</span><span class="sxs-lookup"><span data-stu-id="4863f-120">If you need to preserve the SAS keys, use the `New-AzureRmServiceBuskey` cmdlet with the optional parameter `-Keyvalue` to accept the key as string.</span></span> <span data-ttu-id="4863f-121">The updated cmdlet is available at [PowerShell Gallery release 6.4.0 (July 2018)](https://www.powershellgallery.com/packages/AzureRM/6.4.0) or at [GitHub](https://github.com/Azure/azure-powershell/releases/tag/v6.4.0-July2018).</span><span class="sxs-lookup"><span data-stu-id="4863f-121">The updated cmdlet is available at [PowerShell Gallery release 6.4.0 (July 2018)](https://www.powershellgallery.com/packages/AzureRM/6.4.0) or at [GitHub](https://github.com/Azure/azure-powershell/releases/tag/v6.4.0-July2018).</span></span>

### <a name="usage-example"></a><span data-ttu-id="4863f-122">Usage example</span><span class="sxs-lookup"><span data-stu-id="4863f-122">Usage example</span></span>

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Queue <queuename> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Topic <topicname> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

> [!NOTE]
> <span data-ttu-id="4863f-123">You will need to update your applications to use a new connection string even if you preserve the keys because the DNS host names are different between Azure Germany and global Azure.</span><span class="sxs-lookup"><span data-stu-id="4863f-123">You will need to update your applications to use a new connection string even if you preserve the keys because the DNS host names are different between Azure Germany and global Azure.</span></span>

### <a name="sample-connection-strings"></a><span data-ttu-id="4863f-124">Sample connection strings</span><span class="sxs-lookup"><span data-stu-id="4863f-124">Sample connection strings</span></span>

<span data-ttu-id="4863f-125">**Azure Germany**</span><span class="sxs-lookup"><span data-stu-id="4863f-125">**Azure Germany**</span></span>

```cmd
Endpoint=sb://myBFProdnamespaceName.**servicebus.cloudapi.de**/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXx=
```

<span data-ttu-id="4863f-126">**Global Azure**</span><span class="sxs-lookup"><span data-stu-id="4863f-126">**Global Azure**</span></span>

```cmd
Endpoint=sb://myProdnamespaceName.**servicebus.windows.net**/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXx=
```

### <a name="next-steps"></a><span data-ttu-id="4863f-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="4863f-127">Next steps</span></span>

- <span data-ttu-id="4863f-128">Refresh your knowledge about Service Bus by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/service-bus-messaging/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4863f-128">Refresh your knowledge about Service Bus by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/service-bus-messaging/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="4863f-129">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4863f-129">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="4863f-130">References</span><span class="sxs-lookup"><span data-stu-id="4863f-130">References</span></span>

- [<span data-ttu-id="4863f-131">Service Bus Overview</span><span class="sxs-lookup"><span data-stu-id="4863f-131">Service Bus Overview</span></span>](../service-bus-messaging/service-bus-messaging-overview.md)
- [<span data-ttu-id="4863f-132">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4863f-132">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)







## <a name="logic-apps"></a><span data-ttu-id="4863f-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4863f-133">Logic Apps</span></span>

<span data-ttu-id="4863f-134">Logic Apps service isn't available in Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="4863f-134">Logic Apps service isn't available in Azure Germany.</span></span> <span data-ttu-id="4863f-135">However, Azure Scheduler (which is available) is being deprecated.</span><span class="sxs-lookup"><span data-stu-id="4863f-135">However, Azure Scheduler (which is available) is being deprecated.</span></span> <span data-ttu-id="4863f-136">Use Azure Logic apps instead to create scheduling jobs.</span><span class="sxs-lookup"><span data-stu-id="4863f-136">Use Azure Logic apps instead to create scheduling jobs.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4863f-137">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4863f-137">Next Steps</span></span>

- <span data-ttu-id="4863f-138">Make yourself familiar with the features that [Azure Logic Apps provides by following the [Step-by-Step tutorials](https://docs.microsoft.com/azure/logic-apps/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4863f-138">Make yourself familiar with the features that [Azure Logic Apps provides by following the [Step-by-Step tutorials](https://docs.microsoft.com/azure/logic-apps/#step-by-step-tutorials).</span></span>

### <a name="reference"></a><span data-ttu-id="4863f-139">Reference</span><span class="sxs-lookup"><span data-stu-id="4863f-139">Reference</span></span>

- [<span data-ttu-id="4863f-140">Azure Logic Apps overview</span><span class="sxs-lookup"><span data-stu-id="4863f-140">Azure Logic Apps overview</span></span>](../logic-apps/logic-apps-overview.md) 