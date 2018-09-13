---
title: Microsoft Azure StorSimple and Cloud Solutions Provider Program Overview | Microsoft Docs
description: An overview about the StorSimple and CSP for StorSimple partners.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: a96d2a4749fa5b88cf5f55443be7c618350ce368
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563554"
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="a516d-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span><span class="sxs-lookup"><span data-stu-id="a516d-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="a516d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a516d-104">Overview</span></span>

<span data-ttu-id="a516d-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span><span class="sxs-lookup"><span data-stu-id="a516d-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="a516d-106">A CSP partner can create a StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="a516d-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="a516d-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span><span class="sxs-lookup"><span data-stu-id="a516d-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="a516d-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span><span class="sxs-lookup"><span data-stu-id="a516d-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a516d-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a516d-109">Prerequisites</span></span>

<span data-ttu-id="a516d-110">Before you begin, ensure that:</span><span class="sxs-lookup"><span data-stu-id="a516d-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="a516d-111">You are enrolled under the CSP program.</span><span class="sxs-lookup"><span data-stu-id="a516d-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="a516d-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span><span class="sxs-lookup"><span data-stu-id="a516d-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="a516d-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span><span class="sxs-lookup"><span data-stu-id="a516d-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="a516d-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a516d-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="a516d-115">Add a customer</span><span class="sxs-lookup"><span data-stu-id="a516d-115">Add a customer</span></span>

<span data-ttu-id="a516d-116">If you add a customer, a subscription is automatically created.</span><span class="sxs-lookup"><span data-stu-id="a516d-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="a516d-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span><span class="sxs-lookup"><span data-stu-id="a516d-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="a516d-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span><span class="sxs-lookup"><span data-stu-id="a516d-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="a516d-119">Click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="a516d-119">Click **Dashboard**.</span></span>

     ![Dashboard in Partner Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="a516d-121">In the left-pane, click **Customers**.</span><span class="sxs-lookup"><span data-stu-id="a516d-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="a516d-122">In the right-pane, click **Add customers**.</span><span class="sxs-lookup"><span data-stu-id="a516d-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="a516d-123">Enter the details of the customer.</span><span class="sxs-lookup"><span data-stu-id="a516d-123">Enter the details of the customer.</span></span> <span data-ttu-id="a516d-124">Click **Next: Subscriptions** to create a customer subscription.</span><span class="sxs-lookup"><span data-stu-id="a516d-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Add customer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="a516d-126">Select **Microsoft Azure** offer.</span><span class="sxs-lookup"><span data-stu-id="a516d-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="a516d-127">Scroll to the bottom of the page and click **Review**.</span><span class="sxs-lookup"><span data-stu-id="a516d-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Review subscription information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="a516d-129">Review the information and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="a516d-129">Review the information and click **Submit**.</span></span>

    ![Submit subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="a516d-131">Save the confirmation information for future reference.</span><span class="sxs-lookup"><span data-stu-id="a516d-131">Save the confirmation information for future reference.</span></span>

    ![Save confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="a516d-133">Find or navigate to the customer you just added.</span><span class="sxs-lookup"><span data-stu-id="a516d-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="a516d-134">Click the **Company name** to drill down into the details.</span><span class="sxs-lookup"><span data-stu-id="a516d-134">Click the **Company name** to drill down into the details.</span></span>

    ![Search for the customer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="a516d-136">In the left-pane, select **Service management**.</span><span class="sxs-lookup"><span data-stu-id="a516d-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="a516d-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span><span class="sxs-lookup"><span data-stu-id="a516d-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Log in to Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="a516d-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span><span class="sxs-lookup"><span data-stu-id="a516d-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="a516d-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="a516d-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Create StorSimple Device Manager service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="a516d-142">Add a subscription</span><span class="sxs-lookup"><span data-stu-id="a516d-142">Add a subscription</span></span>

<span data-ttu-id="a516d-143">In some instances, you may have an existing customer, and you need to add a subscription.</span><span class="sxs-lookup"><span data-stu-id="a516d-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="a516d-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span><span class="sxs-lookup"><span data-stu-id="a516d-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="a516d-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span><span class="sxs-lookup"><span data-stu-id="a516d-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="a516d-146">Click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="a516d-146">Click **Dashboard**.</span></span>

     ![Dashboard in Partner Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="a516d-148">In the left-pane, click **Customers**.</span><span class="sxs-lookup"><span data-stu-id="a516d-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="a516d-149">Find or navigate to the customer you want to add a subscription to.</span><span class="sxs-lookup"><span data-stu-id="a516d-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="a516d-150">Click the ![Expand check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span><span class="sxs-lookup"><span data-stu-id="a516d-150">Click the ![Expand check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="a516d-151">In the details, click **Add subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="a516d-151">In the details, click **Add subscriptions**.</span></span>

    ![Customers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="a516d-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="a516d-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="a516d-154">This creates a new subscription.</span><span class="sxs-lookup"><span data-stu-id="a516d-154">This creates a new subscription.</span></span>

    ![Add new subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="a516d-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span><span class="sxs-lookup"><span data-stu-id="a516d-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="a516d-157">Search for the customer for whom you just created a subscription.</span><span class="sxs-lookup"><span data-stu-id="a516d-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="a516d-158">Click the **Company name** to drill down into the details.</span><span class="sxs-lookup"><span data-stu-id="a516d-158">Click the **Company name** to drill down into the details.</span></span>

    ![Search for the customer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="a516d-160">In the left-pane, select **Service management**.</span><span class="sxs-lookup"><span data-stu-id="a516d-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="a516d-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span><span class="sxs-lookup"><span data-stu-id="a516d-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Log in to Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="a516d-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span><span class="sxs-lookup"><span data-stu-id="a516d-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="a516d-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="a516d-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Create StorSimple Device Manager service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="a516d-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="a516d-166">Next steps</span></span>

- <span data-ttu-id="a516d-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a516d-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="a516d-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a516d-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>














