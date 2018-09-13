---
title: Can't sign in to Azure subscription | Microsoft Docs
description: Describes how to troubleshoot some common Azure subscription login issues.
services: ''
documentationcenter: ''
author: genlin
manager: jlian
editor: ''
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genli
ms.openlocfilehash: dd34cf49eb3332370c91cae1ae4792804feaee08
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563095"
---
# <a name="i-cant-sign-in-to-manage-my-azure-subscription"></a><span data-ttu-id="47f9b-103">I can't sign in to manage my Azure subscription</span><span class="sxs-lookup"><span data-stu-id="47f9b-103">I can't sign in to manage my Azure subscription</span></span>
<span data-ttu-id="47f9b-104">This article guides you through some of the most common methods to resolve login issues.</span><span class="sxs-lookup"><span data-stu-id="47f9b-104">This article guides you through some of the most common methods to resolve login issues.</span></span>

## <a name="page-hangs-in-the-loading-status"></a><span data-ttu-id="47f9b-105">Page hangs in the loading status</span><span class="sxs-lookup"><span data-stu-id="47f9b-105">Page hangs in the loading status</span></span>
<span data-ttu-id="47f9b-106">If your internet browser page hangs, try each of the following steps until you can get to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47f9b-106">If your internet browser page hangs, try each of the following steps until you can get to the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="47f9b-107">Refresh the page.</span><span class="sxs-lookup"><span data-stu-id="47f9b-107">Refresh the page.</span></span>
* <span data-ttu-id="47f9b-108">Use a different Internet browser.</span><span class="sxs-lookup"><span data-stu-id="47f9b-108">Use a different Internet browser.</span></span>
* <span data-ttu-id="47f9b-109">If you’re using Microsoft Internet Explorer, browse to the Azure portal by using the InPrivate Browsing mode.</span><span class="sxs-lookup"><span data-stu-id="47f9b-109">If you’re using Microsoft Internet Explorer, browse to the Azure portal by using the InPrivate Browsing mode.</span></span> 
  
  <span data-ttu-id="47f9b-110">A.</span><span class="sxs-lookup"><span data-stu-id="47f9b-110">A.</span></span> <span data-ttu-id="47f9b-111">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-111">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span></span>
  
  <span data-ttu-id="47f9b-112">B.</span><span class="sxs-lookup"><span data-stu-id="47f9b-112">B.</span></span> <span data-ttu-id="47f9b-113">Browse to the [Azure portal](https://portal.azure.com), and then sign in to the portal.</span><span class="sxs-lookup"><span data-stu-id="47f9b-113">Browse to the [Azure portal](https://portal.azure.com), and then sign in to the portal.</span></span>

## <a name="error-message-no-subscriptions-found"></a><span data-ttu-id="47f9b-114">Error message "No subscriptions found”</span><span class="sxs-lookup"><span data-stu-id="47f9b-114">Error message "No subscriptions found”</span></span>
<span data-ttu-id="47f9b-115">If your account doesn’t have sufficient permissions, you may see a **No subscription found** error message.</span><span class="sxs-lookup"><span data-stu-id="47f9b-115">If your account doesn’t have sufficient permissions, you may see a **No subscription found** error message.</span></span> <span data-ttu-id="47f9b-116">Make sure you log in as the right administrator.</span><span class="sxs-lookup"><span data-stu-id="47f9b-116">Make sure you log in as the right administrator.</span></span> <span data-ttu-id="47f9b-117">An Account Administrator can only access the [Account Center](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="47f9b-117">An Account Administrator can only access the [Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="47f9b-118">The Service Administrators (SA) and Co-Administrators (CA) only have access to the [Azure portal](https://portal.azure.com) or the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="47f9b-118">The Service Administrators (SA) and Co-Administrators (CA) only have access to the [Azure portal](https://portal.azure.com) or the Azure classic portal.</span></span>

<span data-ttu-id="47f9b-119">**Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)**</span><span class="sxs-lookup"><span data-stu-id="47f9b-119">**Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)**</span></span>

<span data-ttu-id="47f9b-120">To fix this issue:</span><span class="sxs-lookup"><span data-stu-id="47f9b-120">To fix this issue:</span></span>

* <span data-ttu-id="47f9b-121">Make sure the right Azure directory is selected by clicking your account at the top right.</span><span class="sxs-lookup"><span data-stu-id="47f9b-121">Make sure the right Azure directory is selected by clicking your account at the top right.</span></span>

![Select the directory at the top right of the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/directory-switch.png)

* <span data-ttu-id="47f9b-123">If the right Azure directory is selected but you still get the error, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="47f9b-123">If the right Azure directory is selected but you still get the error, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="47f9b-124">**Scenario 2: Error message is received in the [Azure Account Center](https://account.windowsazure.com/Subscriptions)**</span><span class="sxs-lookup"><span data-stu-id="47f9b-124">**Scenario 2: Error message is received in the [Azure Account Center](https://account.windowsazure.com/Subscriptions)**</span></span>

<span data-ttu-id="47f9b-125">Check whether the account that you used is the account administrator.</span><span class="sxs-lookup"><span data-stu-id="47f9b-125">Check whether the account that you used is the account administrator.</span></span> <span data-ttu-id="47f9b-126">To verify who the account administrator is, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="47f9b-126">To verify who the account administrator is, follow these steps:</span></span>

1. <span data-ttu-id="47f9b-127">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47f9b-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47f9b-128">On the Hub menu, select **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-128">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="47f9b-129">Select the subscription that you want to check, and then select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-129">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="47f9b-130">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-130">Select **Properties**.</span></span> <span data-ttu-id="47f9b-131">The account administrator of the subscription is displayed in the **Account Admin** box.</span><span class="sxs-lookup"><span data-stu-id="47f9b-131">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="you-are-automatically-signed-in-as-a-different-user"></a><span data-ttu-id="47f9b-132">You are automatically signed in as a different user</span><span class="sxs-lookup"><span data-stu-id="47f9b-132">You are automatically signed in as a different user</span></span>
<span data-ttu-id="47f9b-133">This issue can occur if you use more than one user account in an Internet browser.</span><span class="sxs-lookup"><span data-stu-id="47f9b-133">This issue can occur if you use more than one user account in an Internet browser.</span></span>

<span data-ttu-id="47f9b-134">To resolve the issue, try one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="47f9b-134">To resolve the issue, try one of the following methods:</span></span>

* <span data-ttu-id="47f9b-135">Clear the cache and delete Internet cookies.</span><span class="sxs-lookup"><span data-stu-id="47f9b-135">Clear the cache and delete Internet cookies.</span></span> <span data-ttu-id="47f9b-136">In Internet Explorer, click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Internet Options** > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-136">In Internet Explorer, click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Internet Options** > **Delete**.</span></span> <span data-ttu-id="47f9b-137">Make sure that the check boxes for temporary files, cookies, password, and browsing history are selected, and then click Delete.</span><span class="sxs-lookup"><span data-stu-id="47f9b-137">Make sure that the check boxes for temporary files, cookies, password, and browsing history are selected, and then click Delete.</span></span>
* <span data-ttu-id="47f9b-138">Reset the Internet Explorer settings to revert any personal settings that you’ve made.</span><span class="sxs-lookup"><span data-stu-id="47f9b-138">Reset the Internet Explorer settings to revert any personal settings that you’ve made.</span></span> <span data-ttu-id="47f9b-139">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png)> **Internet Options** > **Advanced** >select the **Delete personal settings** box > **Reset**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-139">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png)> **Internet Options** > **Advanced** >select the **Delete personal settings** box > **Reset**.</span></span>
* <span data-ttu-id="47f9b-140">Browse to the Azure portal in InPrivate Browsing mode.</span><span class="sxs-lookup"><span data-stu-id="47f9b-140">Browse to the Azure portal in InPrivate Browsing mode.</span></span> <span data-ttu-id="47f9b-141">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span><span class="sxs-lookup"><span data-stu-id="47f9b-141">Click **Tools** ![tools button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="47f9b-142">Need help?</span><span class="sxs-lookup"><span data-stu-id="47f9b-142">Need help?</span></span> <span data-ttu-id="47f9b-143">Contact support.</span><span class="sxs-lookup"><span data-stu-id="47f9b-143">Contact support.</span></span>
<span data-ttu-id="47f9b-144">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="47f9b-144">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 






