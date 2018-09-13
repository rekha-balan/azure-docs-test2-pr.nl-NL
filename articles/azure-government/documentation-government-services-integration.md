---
title: Azure Government Developer Tools | Microsoft Docs
description: This provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: gsacavdm
manager: pathuff
ms.assetid: afef7a1b-7abb-4073-8b3f-b7f7a49e000f
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 6/13/2018
ms.author: gsacavdm
ms.openlocfilehash: c1f91fc8b27dcfc9145a834251e4f6ad39036257
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857022"
---
# <a name="azure-government-integration-services"></a><span data-ttu-id="87316-103">Azure Government Integration Services</span><span class="sxs-lookup"><span data-stu-id="87316-103">Azure Government Integration Services</span></span>
<span data-ttu-id="87316-104">This article outlines the integration services variations and considerations for the Azure Government environment.</span><span class="sxs-lookup"><span data-stu-id="87316-104">This article outlines the integration services variations and considerations for the Azure Government environment.</span></span>

## <a name="logic-apps"></a><span data-ttu-id="87316-105">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="87316-105">Logic Apps</span></span>
<span data-ttu-id="87316-106">Logic Apps is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="87316-106">Logic Apps is generally available in Azure Government.</span></span>
<span data-ttu-id="87316-107">For more information, see [Logic Apps public documentation](../logic-apps/logic-apps-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87316-107">For more information, see [Logic Apps public documentation](../logic-apps/logic-apps-overview.md).</span></span>

### <a name="variations"></a><span data-ttu-id="87316-108">Variations</span><span class="sxs-lookup"><span data-stu-id="87316-108">Variations</span></span>
* <span data-ttu-id="87316-109">The Azure-based [Connectors](../connectors/apis-list.md) are scoped to connect to resources in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="87316-109">The Azure-based [Connectors](../connectors/apis-list.md) are scoped to connect to resources in Azure Government.</span></span> <span data-ttu-id="87316-110">If the Azure service isn't yet available in Azure Government, the connector for that service isn't available, for example:</span><span class="sxs-lookup"><span data-stu-id="87316-110">If the Azure service isn't yet available in Azure Government, the connector for that service isn't available, for example:</span></span>
    * <span data-ttu-id="87316-111">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="87316-111">Data Lake Store</span></span>
    * <span data-ttu-id="87316-112">Data Factory</span><span class="sxs-lookup"><span data-stu-id="87316-112">Data Factory</span></span>
    * <span data-ttu-id="87316-113">Event Grid</span><span class="sxs-lookup"><span data-stu-id="87316-113">Event Grid</span></span>
    * <span data-ttu-id="87316-114">Application Insights</span><span class="sxs-lookup"><span data-stu-id="87316-114">Application Insights</span></span>
    * <span data-ttu-id="87316-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="87316-115">Content Moderator</span></span>

* <span data-ttu-id="87316-116">For other missing connectors, request them via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government) and the [Logic Apps feedback forum](https://feedback.azure.com/forums/287593-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="87316-116">For other missing connectors, request them via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government) and the [Logic Apps feedback forum](https://feedback.azure.com/forums/287593-logic-apps).</span></span> <span data-ttu-id="87316-117">If you need to use any missing connectors, you can call a logic app hosted in Azure Commercial that uses them.</span><span class="sxs-lookup"><span data-stu-id="87316-117">If you need to use any missing connectors, you can call a logic app hosted in Azure Commercial that uses them.</span></span>

* <span data-ttu-id="87316-118">The creation experience for custom connectors via the portal isn't yet available.</span><span class="sxs-lookup"><span data-stu-id="87316-118">The creation experience for custom connectors via the portal isn't yet available.</span></span> <span data-ttu-id="87316-119">If you need to use the portal experience to create a custom connector, you can leverage the portal experience in Azure Commercial.</span><span class="sxs-lookup"><span data-stu-id="87316-119">If you need to use the portal experience to create a custom connector, you can leverage the portal experience in Azure Commercial.</span></span> <span data-ttu-id="87316-120">Create the resource in Azure Commercial, download it as an Azure Resource Manager deployment template, and deploy it to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="87316-120">Create the resource in Azure Commercial, download it as an Azure Resource Manager deployment template, and deploy it to Azure Government.</span></span> <span data-ttu-id="87316-121">You can download a custom connector by selecting the Download button on the Logic Apps Custom Connector overview blade.</span><span class="sxs-lookup"><span data-stu-id="87316-121">You can download a custom connector by selecting the Download button on the Logic Apps Custom Connector overview blade.</span></span> <span data-ttu-id="87316-122">To deploy resources in a Resource Manager deployment template from the Azure portal, see the [resource group deployment documentation](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template).</span><span class="sxs-lookup"><span data-stu-id="87316-122">To deploy resources in a Resource Manager deployment template from the Azure portal, see the [resource group deployment documentation](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87316-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="87316-123">Next steps</span></span>
* <span data-ttu-id="87316-124">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="87316-124">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="87316-125">Get help on Stack Overflow by using the [azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)</span><span class="sxs-lookup"><span data-stu-id="87316-125">Get help on Stack Overflow by using the [azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)</span></span>
* <span data-ttu-id="87316-126">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="87316-126">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span> 
