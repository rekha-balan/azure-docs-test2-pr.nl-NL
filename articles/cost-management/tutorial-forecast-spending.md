---
title: Tutorial - Forecast spending with Azure Cost Management | Microsoft Docs
description: In this tutorial you learn how to forecast spending using historical usage and spending data.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 04/26/2018
ms.topic: tutorial
ms.service: cost-management
ms.custom: ''
manager: dougeby
ms.openlocfilehash: 411b4797510b26dec43ea7f2232457199808c857
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868330"
---
# <a name="tutorial-forecast-future-spending"></a><span data-ttu-id="7fe13-103">Tutorial: Forecast future spending</span><span class="sxs-lookup"><span data-stu-id="7fe13-103">Tutorial: Forecast future spending</span></span>

<span data-ttu-id="7fe13-104">Azure Cost Management helps you forecast future spending using historical usage and spending data.</span><span class="sxs-lookup"><span data-stu-id="7fe13-104">Azure Cost Management helps you forecast future spending using historical usage and spending data.</span></span> <span data-ttu-id="7fe13-105">You use Cloudyn reports to view all cost projection data.</span><span class="sxs-lookup"><span data-stu-id="7fe13-105">You use Cloudyn reports to view all cost projection data.</span></span> <span data-ttu-id="7fe13-106">The examples in this tutorial walk you through reviewing cost projections using the reports.</span><span class="sxs-lookup"><span data-stu-id="7fe13-106">The examples in this tutorial walk you through reviewing cost projections using the reports.</span></span> <span data-ttu-id="7fe13-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="7fe13-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fe13-108">Forecast future spending</span><span class="sxs-lookup"><span data-stu-id="7fe13-108">Forecast future spending</span></span>

<span data-ttu-id="7fe13-109">If you don't have an Azure subscription, create a  [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="7fe13-109">If you don't have an Azure subscription, create a  [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fe13-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7fe13-110">Prerequisites</span></span>

- <span data-ttu-id="7fe13-111">You must have an Azure account.</span><span class="sxs-lookup"><span data-stu-id="7fe13-111">You must have an Azure account.</span></span>
- <span data-ttu-id="7fe13-112">You must have either a trial registration or paid subscription for Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7fe13-112">You must have either a trial registration or paid subscription for Azure Cost Management.</span></span>

## <a name="forecast-future-spending"></a><span data-ttu-id="7fe13-113">Forecast future spending</span><span class="sxs-lookup"><span data-stu-id="7fe13-113">Forecast future spending</span></span>

<span data-ttu-id="7fe13-114">Cloudyn includes cost projection reports to help you forecast spending based on your usage over time.</span><span class="sxs-lookup"><span data-stu-id="7fe13-114">Cloudyn includes cost projection reports to help you forecast spending based on your usage over time.</span></span> <span data-ttu-id="7fe13-115">Their primary purpose is to help you ensure that your cost trends do not exceed your organization's expectations.</span><span class="sxs-lookup"><span data-stu-id="7fe13-115">Their primary purpose is to help you ensure that your cost trends do not exceed your organization's expectations.</span></span> <span data-ttu-id="7fe13-116">The reports you use are Current Month Projected Cost and Annual Projected Cost.</span><span class="sxs-lookup"><span data-stu-id="7fe13-116">The reports you use are Current Month Projected Cost and Annual Projected Cost.</span></span> <span data-ttu-id="7fe13-117">Both show projected future spending if your usage remains relatively consistent with your last 30 days of usage.</span><span class="sxs-lookup"><span data-stu-id="7fe13-117">Both show projected future spending if your usage remains relatively consistent with your last 30 days of usage.</span></span>

<span data-ttu-id="7fe13-118">The Current Month Projected Cost report shows the costs of your services.</span><span class="sxs-lookup"><span data-stu-id="7fe13-118">The Current Month Projected Cost report shows the costs of your services.</span></span> <span data-ttu-id="7fe13-119">It uses costs from the beginning of the month and the previous month to show the projected cost.</span><span class="sxs-lookup"><span data-stu-id="7fe13-119">It uses costs from the beginning of the month and the previous month to show the projected cost.</span></span> <span data-ttu-id="7fe13-120">On the reports menu at the top of the portal, click **Cost** > **Projection and Budget** > **Current Month Projected Cost**.</span><span class="sxs-lookup"><span data-stu-id="7fe13-120">On the reports menu at the top of the portal, click **Cost** > **Projection and Budget** > **Current Month Projected Cost**.</span></span> <span data-ttu-id="7fe13-121">The following image shows an example.</span><span class="sxs-lookup"><span data-stu-id="7fe13-121">The following image shows an example.</span></span>

![current month projected cost](./media/tutorial-forecast-spending/project-month01.png)

<span data-ttu-id="7fe13-123">In the example, you can see which services spent the most.</span><span class="sxs-lookup"><span data-stu-id="7fe13-123">In the example, you can see which services spent the most.</span></span> <span data-ttu-id="7fe13-124">Azure costs were lower than AWS costs.</span><span class="sxs-lookup"><span data-stu-id="7fe13-124">Azure costs were lower than AWS costs.</span></span> <span data-ttu-id="7fe13-125">If you want to see cost projection details for Azure VMs, in the **Filter** list, select **Azure/VM**.</span><span class="sxs-lookup"><span data-stu-id="7fe13-125">If you want to see cost projection details for Azure VMs, in the **Filter** list, select **Azure/VM**.</span></span>

![Azure VM current month projected cost](./media/tutorial-forecast-spending/project-month02.png)

<span data-ttu-id="7fe13-127">Follow the same basic preceding steps to look at monthly cost projections for other services you're interested in.</span><span class="sxs-lookup"><span data-stu-id="7fe13-127">Follow the same basic preceding steps to look at monthly cost projections for other services you're interested in.</span></span>

<span data-ttu-id="7fe13-128">The Annual Projected Cost report shows the extrapolated cost of your services over the next 12 months.</span><span class="sxs-lookup"><span data-stu-id="7fe13-128">The Annual Projected Cost report shows the extrapolated cost of your services over the next 12 months.</span></span>

<span data-ttu-id="7fe13-129">On the reports menu at the top of the portal, click **Cost** > **Projection and Budget** > **Annual Projected Cost**.</span><span class="sxs-lookup"><span data-stu-id="7fe13-129">On the reports menu at the top of the portal, click **Cost** > **Projection and Budget** > **Annual Projected Cost**.</span></span> <span data-ttu-id="7fe13-130">The following image shows an example.</span><span class="sxs-lookup"><span data-stu-id="7fe13-130">The following image shows an example.</span></span>

![annual projected cost report](./media/tutorial-forecast-spending/project-annual01.png)

<span data-ttu-id="7fe13-132">In the example, you can see which services spent the most.</span><span class="sxs-lookup"><span data-stu-id="7fe13-132">In the example, you can see which services spent the most.</span></span> <span data-ttu-id="7fe13-133">Like the monthly example, Azure costs were lower than AWS costs.</span><span class="sxs-lookup"><span data-stu-id="7fe13-133">Like the monthly example, Azure costs were lower than AWS costs.</span></span> <span data-ttu-id="7fe13-134">If you want to see cost projection details for Azure VMs, in the **Filter** list, select **Azure/VM**.</span><span class="sxs-lookup"><span data-stu-id="7fe13-134">If you want to see cost projection details for Azure VMs, in the **Filter** list, select **Azure/VM**.</span></span>

![annual projected cost of VMs](./media/tutorial-forecast-spending/project-annual02.png)

<span data-ttu-id="7fe13-136">In the image above, the annual projected cost of Azure VMs is $28,374.</span><span class="sxs-lookup"><span data-stu-id="7fe13-136">In the image above, the annual projected cost of Azure VMs is $28,374.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe13-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fe13-137">Next steps</span></span>

<span data-ttu-id="7fe13-138">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="7fe13-138">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fe13-139">Forecast future spending</span><span class="sxs-lookup"><span data-stu-id="7fe13-139">Forecast future spending</span></span>


<span data-ttu-id="7fe13-140">Advance to the next tutorial to learn how to manage costs with cost allocation and showback reports.</span><span class="sxs-lookup"><span data-stu-id="7fe13-140">Advance to the next tutorial to learn how to manage costs with cost allocation and showback reports.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fe13-141">Manage costs with cost allocation and showback reports</span><span class="sxs-lookup"><span data-stu-id="7fe13-141">Manage costs with cost allocation and showback reports</span></span>](tutorial-manage-costs.md)
