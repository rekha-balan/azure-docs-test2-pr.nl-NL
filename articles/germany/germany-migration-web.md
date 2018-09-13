---
title: Migration of web resources from Azure Germany to global Azure
description: This article provides help for migrating web resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 8c5bae86636774b23da5507936e3dd0002538f05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870636"
---
# <a name="migration-of-web-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="c7a3b-103">Migration of web resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-103">Migration of web resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="c7a3b-104">This article will provide you some help for the migration of Azure Web resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-104">This article will provide you some help for the migration of Azure Web resources from Azure Germany to global Azure.</span></span>

## <a name="app-service---web-apps"></a><span data-ttu-id="c7a3b-105">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="c7a3b-105">App Service - Web Apps</span></span>

<span data-ttu-id="c7a3b-106">The migration of App Services from Azure Germany to global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-106">The migration of App Services from Azure Germany to global Azure isn't supported at this time.</span></span> <span data-ttu-id="c7a3b-107">The recommended approach is to export as Resource Manager template and redeploy after changing the location property to the new destination region.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-107">The recommended approach is to export as Resource Manager template and redeploy after changing the location property to the new destination region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7a3b-108">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-108">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c7a3b-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7a3b-109">Next steps</span></span>

- <span data-ttu-id="c7a3b-110">Refresh your knowledge about App Services by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/app-service/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-110">Refresh your knowledge about App Services by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/app-service/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="c7a3b-111">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-111">Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>

### <a name="references"></a><span data-ttu-id="c7a3b-112">References</span><span class="sxs-lookup"><span data-stu-id="c7a3b-112">References</span></span>

- [<span data-ttu-id="c7a3b-113">App Service Overview</span><span class="sxs-lookup"><span data-stu-id="c7a3b-113">App Service Overview</span></span>](../app-service/app-service-web-overview.md)
- [<span data-ttu-id="c7a3b-114">Export a Resource Manager template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7a3b-114">Export a Resource Manager template using PowerShell</span></span>](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)
- [<span data-ttu-id="c7a3b-115">Overview of Azure locations</span><span class="sxs-lookup"><span data-stu-id="c7a3b-115">Overview of Azure locations</span></span>](https://azure.microsoft.com/global-infrastructure/locations/)
- [<span data-ttu-id="c7a3b-116">Redeploy a template</span><span class="sxs-lookup"><span data-stu-id="c7a3b-116">Redeploy a template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)












## <a name="notification-hubs"></a><span data-ttu-id="c7a3b-117">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="c7a3b-117">Notification Hubs</span></span>

<span data-ttu-id="c7a3b-118">To migrate settings from one Notification Hub to another, you can export and import all registration tokens along with tags.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-118">To migrate settings from one Notification Hub to another, you can export and import all registration tokens along with tags.</span></span> <span data-ttu-id="c7a3b-119">Here's how:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-119">Here's how:</span></span>

- <span data-ttu-id="c7a3b-120">[Export the existing Hub registrations](https://msdn.microsoft.com/library/azure/dn790624.aspx) into an Azure Blob Storage container.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-120">[Export the existing Hub registrations](https://msdn.microsoft.com/library/azure/dn790624.aspx) into an Azure Blob Storage container.</span></span>
- <span data-ttu-id="c7a3b-121">Create a new Notification Hub in the target environment</span><span class="sxs-lookup"><span data-stu-id="c7a3b-121">Create a new Notification Hub in the target environment</span></span>
- <span data-ttu-id="c7a3b-122">[Import your Registration Tokens](https://msdn.microsoft.com/library/azure/dn790624.aspx) from Azure Blob Storage to your new Hub</span><span class="sxs-lookup"><span data-stu-id="c7a3b-122">[Import your Registration Tokens](https://msdn.microsoft.com/library/azure/dn790624.aspx) from Azure Blob Storage to your new Hub</span></span>

### <a name="next-steps"></a><span data-ttu-id="c7a3b-123">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c7a3b-123">Next Steps</span></span>

<span data-ttu-id="c7a3b-124">Refresh your knowledge about Notification Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/notification-hubs/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-124">Refresh your knowledge about Notification Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/notification-hubs/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="c7a3b-125">References</span><span class="sxs-lookup"><span data-stu-id="c7a3b-125">References</span></span>

- [<span data-ttu-id="c7a3b-126">Notification Hubs overview</span><span class="sxs-lookup"><span data-stu-id="c7a3b-126">Notification Hubs overview</span></span>](../notification-hubs/notification-hubs-push-notification-overview.md)