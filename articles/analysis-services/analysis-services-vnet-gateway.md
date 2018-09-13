---
title: Use On-premises data gateway for Azure Virtual Network data sources | Microsoft Docs
description: Learn how to configure a server to use a gateway for data sources on VNet.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: f1cf447f27509bc62cc71a9c64237ff7dc3d7b30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871427"
---
# <a name="use-gateway-for-data-sources-on-an-azure-virtual-network-vnet"></a><span data-ttu-id="a7928-103">Use gateway for data sources on an Azure Virtual Network (VNet)</span><span class="sxs-lookup"><span data-stu-id="a7928-103">Use gateway for data sources on an Azure Virtual Network (VNet)</span></span>

<span data-ttu-id="a7928-104">This article describes the **AlwaysUseGateway** server property for use when data sources are on an [Azure Virtual Network (VNet)](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7928-104">This article describes the **AlwaysUseGateway** server property for use when data sources are on an [Azure Virtual Network (VNet)](../virtual-network/virtual-networks-overview.md).</span></span>

## <a name="server-access-to-vnet-data-sources"></a><span data-ttu-id="a7928-105">Server access to VNet data sources</span><span class="sxs-lookup"><span data-stu-id="a7928-105">Server access to VNet data sources</span></span>

<span data-ttu-id="a7928-106">If your data sources are accessed through a VNet, your Azure Analysis Services server must connect to those data sources as if they are on-premises, in your own environment.</span><span class="sxs-lookup"><span data-stu-id="a7928-106">If your data sources are accessed through a VNet, your Azure Analysis Services server must connect to those data sources as if they are on-premises, in your own environment.</span></span> <span data-ttu-id="a7928-107">You can configure the **AlwaysUseGateway** server property to specify the server to access all datasource data through an [On-premises gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a7928-107">You can configure the **AlwaysUseGateway** server property to specify the server to access all datasource data through an [On-premises gateway](analysis-services-gateway.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="a7928-108">This property is effective only when an [On-premises data gateway](analysis-services-gateway.md) is installed and configured.</span><span class="sxs-lookup"><span data-stu-id="a7928-108">This property is effective only when an [On-premises data gateway](analysis-services-gateway.md) is installed and configured.</span></span> <span data-ttu-id="a7928-109">The gateway can be on the VNet.</span><span class="sxs-lookup"><span data-stu-id="a7928-109">The gateway can be on the VNet.</span></span>

## <a name="configure-alwaysusegateway-property"></a><span data-ttu-id="a7928-110">Configure AlwaysUseGateway property</span><span class="sxs-lookup"><span data-stu-id="a7928-110">Configure AlwaysUseGateway property</span></span>

1. <span data-ttu-id="a7928-111">In SSMS > server > **Properties** > **General**, select **Show Advanced (All) Properties**.</span><span class="sxs-lookup"><span data-stu-id="a7928-111">In SSMS > server > **Properties** > **General**, select **Show Advanced (All) Properties**.</span></span>
2. <span data-ttu-id="a7928-112">In the **ASPaaS\AlwaysUseGateway**, select **true**.</span><span class="sxs-lookup"><span data-stu-id="a7928-112">In the **ASPaaS\AlwaysUseGateway**, select **true**.</span></span>

    ![Always use gateway property](media/analysis-services-vnet-gateway/aas-ssms-always-property.png)


## <a name="see-also"></a><span data-ttu-id="a7928-114">See also</span><span class="sxs-lookup"><span data-stu-id="a7928-114">See also</span></span>
<span data-ttu-id="a7928-115">[Connecting to on-premises data sources](analysis-services-gateway.md) </span><span class="sxs-lookup"><span data-stu-id="a7928-115">[Connecting to on-premises data sources](analysis-services-gateway.md) </span></span>  
<span data-ttu-id="a7928-116">[Install and configure an on-premises data gateway](analysis-services-gateway-install.md) </span><span class="sxs-lookup"><span data-stu-id="a7928-116">[Install and configure an on-premises data gateway](analysis-services-gateway-install.md) </span></span>  
[<span data-ttu-id="a7928-117">Azure Virtual Network (VNET)</span><span class="sxs-lookup"><span data-stu-id="a7928-117">Azure Virtual Network (VNET)</span></span>](../virtual-network/virtual-networks-overview.md)   

