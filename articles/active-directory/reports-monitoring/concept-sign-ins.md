---
title: Sign-in activity reports in the Azure Active Directory portal | Microsoft Docs
description: Introduction to sign-in activity reports in the Azure Active Directory portal
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 06/21/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: bc8d3525ab7cdbdf298ecbbc686ced16fa7bc77c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865589"
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="bd733-103">Sign-in activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="bd733-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="bd733-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="bd733-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="bd733-105">The reporting architecture in Azure Active Directory consists of the following components:</span><span class="sxs-lookup"><span data-stu-id="bd733-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="bd733-106">**Activity**</span><span class="sxs-lookup"><span data-stu-id="bd733-106">**Activity**</span></span> 
    - <span data-ttu-id="bd733-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="bd733-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="bd733-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span><span class="sxs-lookup"><span data-stu-id="bd733-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="bd733-109">**Security**</span><span class="sxs-lookup"><span data-stu-id="bd733-109">**Security**</span></span> 
    - <span data-ttu-id="bd733-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="bd733-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="bd733-111">For more details, see Risky sign-ins.</span><span class="sxs-lookup"><span data-stu-id="bd733-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="bd733-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="bd733-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="bd733-113">For more details, see Users flagged for risk.</span><span class="sxs-lookup"><span data-stu-id="bd733-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="bd733-114">This topic gives you an overview of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="bd733-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd733-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bd733-115">Prerequisites</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="bd733-116">Who can access the data?</span><span class="sxs-lookup"><span data-stu-id="bd733-116">Who can access the data?</span></span>
* <span data-ttu-id="bd733-117">Users in the Security Admin, Security Reader, Report Reader role</span><span class="sxs-lookup"><span data-stu-id="bd733-117">Users in the Security Admin, Security Reader, Report Reader role</span></span>
* <span data-ttu-id="bd733-118">Global Admins</span><span class="sxs-lookup"><span data-stu-id="bd733-118">Global Admins</span></span>
* <span data-ttu-id="bd733-119">Any user (non-admins) can access their own sign-ins</span><span class="sxs-lookup"><span data-stu-id="bd733-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="bd733-120">What Azure AD license do you need to access sign-in activity?</span><span class="sxs-lookup"><span data-stu-id="bd733-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="bd733-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span><span class="sxs-lookup"><span data-stu-id="bd733-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="sign-in-activities"></a><span data-ttu-id="bd733-122">Sign-in activities</span><span class="sxs-lookup"><span data-stu-id="bd733-122">Sign-in activities</span></span>

<span data-ttu-id="bd733-123">With the information provided by the user sign-in report, you find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="bd733-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="bd733-124">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="bd733-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="bd733-125">How many users have signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="bd733-125">How many users have signed in over a week?</span></span>
* <span data-ttu-id="bd733-126">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="bd733-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="bd733-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd733-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active Directory**.</span></span>


<span data-ttu-id="bd733-128">![Sign-in activity](./media/concept-sign-ins/61.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-128">![Sign-in activity](./media/concept-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="bd733-129">A sign-ins log has a default list view that shows:</span><span class="sxs-lookup"><span data-stu-id="bd733-129">A sign-ins log has a default list view that shows:</span></span>

- <span data-ttu-id="bd733-130">The sign-in date</span><span class="sxs-lookup"><span data-stu-id="bd733-130">The sign-in date</span></span>
- <span data-ttu-id="bd733-131">The related user</span><span class="sxs-lookup"><span data-stu-id="bd733-131">The related user</span></span>
- <span data-ttu-id="bd733-132">The application the user has signed-in to</span><span class="sxs-lookup"><span data-stu-id="bd733-132">The application the user has signed-in to</span></span>
- <span data-ttu-id="bd733-133">The sign-in status</span><span class="sxs-lookup"><span data-stu-id="bd733-133">The sign-in status</span></span>
- <span data-ttu-id="bd733-134">The status of the risk detection</span><span class="sxs-lookup"><span data-stu-id="bd733-134">The status of the risk detection</span></span>
- <span data-ttu-id="bd733-135">The status of the multi-factor authentication (MFA) requirement</span><span class="sxs-lookup"><span data-stu-id="bd733-135">The status of the multi-factor authentication (MFA) requirement</span></span>

<span data-ttu-id="bd733-136">![Sign-in activity](./media/concept-sign-ins/01.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-136">![Sign-in activity](./media/concept-sign-ins/01.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-137">You can customize the list view by clicking **Columns** in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="bd733-137">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="bd733-138">![Sign-in activity](./media/concept-sign-ins/19.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-138">![Sign-in activity](./media/concept-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-139">This enables you to display additional fields or remove fields that are already displayed.</span><span class="sxs-lookup"><span data-stu-id="bd733-139">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="bd733-140">![Sign-in activity](./media/concept-sign-ins/02.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-140">![Sign-in activity](./media/concept-sign-ins/02.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-141">By clicking an item in the list view, you get all available details about it in a horizontal view.</span><span class="sxs-lookup"><span data-stu-id="bd733-141">By clicking an item in the list view, you get all available details about it in a horizontal view.</span></span>

<span data-ttu-id="bd733-142">![Sign-in activity](./media/concept-sign-ins/03.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-142">![Sign-in activity](./media/concept-sign-ins/03.png "Sign-in activity")</span></span>

> [!NOTE]
> <span data-ttu-id="bd733-143">Customers can now troubleshoot conditional access policies through all sign-in reports.</span><span class="sxs-lookup"><span data-stu-id="bd733-143">Customers can now troubleshoot conditional access policies through all sign-in reports.</span></span> <span data-ttu-id="bd733-144">By clicking on the **Conditional access** tab for a sign-in record, customers can review the conditional access status and dive into the details of the policies that applied to the sign-in and the result for each policy.</span><span class="sxs-lookup"><span data-stu-id="bd733-144">By clicking on the **Conditional access** tab for a sign-in record, customers can review the conditional access status and dive into the details of the policies that applied to the sign-in and the result for each policy.</span></span>
> <span data-ttu-id="bd733-145">For more information, see the [Frequently asked questions about CA information in all sign-ins](reports-faq.md#conditional-access).</span><span class="sxs-lookup"><span data-stu-id="bd733-145">For more information, see the [Frequently asked questions about CA information in all sign-ins](reports-faq.md#conditional-access).</span></span>

<span data-ttu-id="bd733-146">![Sign-in activity](./media/concept-sign-ins/ConditionalAccess.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-146">![Sign-in activity](./media/concept-sign-ins/ConditionalAccess.png "Sign-in activity")</span></span>


## <a name="filter-sign-in-activities"></a><span data-ttu-id="bd733-147">Filter sign-in activities</span><span class="sxs-lookup"><span data-stu-id="bd733-147">Filter sign-in activities</span></span>

<span data-ttu-id="bd733-148">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following default fields:</span><span class="sxs-lookup"><span data-stu-id="bd733-148">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following default fields:</span></span>

- <span data-ttu-id="bd733-149">User</span><span class="sxs-lookup"><span data-stu-id="bd733-149">User</span></span>
- <span data-ttu-id="bd733-150">Application</span><span class="sxs-lookup"><span data-stu-id="bd733-150">Application</span></span>
- <span data-ttu-id="bd733-151">Sign-in status</span><span class="sxs-lookup"><span data-stu-id="bd733-151">Sign-in status</span></span>
- <span data-ttu-id="bd733-152">Status of the risk detection</span><span class="sxs-lookup"><span data-stu-id="bd733-152">Status of the risk detection</span></span>
- <span data-ttu-id="bd733-153">Date</span><span class="sxs-lookup"><span data-stu-id="bd733-153">Date</span></span>

<span data-ttu-id="bd733-154">![Sign-in activity](./media/concept-sign-ins/04.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-154">![Sign-in activity](./media/concept-sign-ins/04.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-155">The **User** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span><span class="sxs-lookup"><span data-stu-id="bd733-155">The **User** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="bd733-156">The **Application** filter enables you to specify the name of the application you care about.</span><span class="sxs-lookup"><span data-stu-id="bd733-156">The **Application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="bd733-157">The **Sign-in status** filter enables you to select:</span><span class="sxs-lookup"><span data-stu-id="bd733-157">The **Sign-in status** filter enables you to select:</span></span>

- <span data-ttu-id="bd733-158">All</span><span class="sxs-lookup"><span data-stu-id="bd733-158">All</span></span>
- <span data-ttu-id="bd733-159">Success</span><span class="sxs-lookup"><span data-stu-id="bd733-159">Success</span></span>
- <span data-ttu-id="bd733-160">Failure</span><span class="sxs-lookup"><span data-stu-id="bd733-160">Failure</span></span>

<span data-ttu-id="bd733-161">The **Risk Detected** filter enables you to select:</span><span class="sxs-lookup"><span data-stu-id="bd733-161">The **Risk Detected** filter enables you to select:</span></span>

- <span data-ttu-id="bd733-162">All</span><span class="sxs-lookup"><span data-stu-id="bd733-162">All</span></span>
- <span data-ttu-id="bd733-163">Yes</span><span class="sxs-lookup"><span data-stu-id="bd733-163">Yes</span></span>
- <span data-ttu-id="bd733-164">No</span><span class="sxs-lookup"><span data-stu-id="bd733-164">No</span></span>

<span data-ttu-id="bd733-165">The **Date** filter enables to you to define a timeframe for the returned data.</span><span class="sxs-lookup"><span data-stu-id="bd733-165">The **Date** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="bd733-166">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="bd733-166">Possible values are:</span></span>

- <span data-ttu-id="bd733-167">1 month</span><span class="sxs-lookup"><span data-stu-id="bd733-167">1 month</span></span>
- <span data-ttu-id="bd733-168">7 days</span><span class="sxs-lookup"><span data-stu-id="bd733-168">7 days</span></span>
- <span data-ttu-id="bd733-169">24 hours</span><span class="sxs-lookup"><span data-stu-id="bd733-169">24 hours</span></span>
- <span data-ttu-id="bd733-170">Custom time interval</span><span class="sxs-lookup"><span data-stu-id="bd733-170">Custom time interval</span></span>

<span data-ttu-id="bd733-171">When you select a custom timeframe, you can configure a start time and an end time.</span><span class="sxs-lookup"><span data-stu-id="bd733-171">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="bd733-172">If you add additional fields to your sign-ins view, these fields are automatically added to the list of filters.</span><span class="sxs-lookup"><span data-stu-id="bd733-172">If you add additional fields to your sign-ins view, these fields are automatically added to the list of filters.</span></span> <span data-ttu-id="bd733-173">For example, by adding **Client App** field to your list, you also get another filter option that enables you to set the following filters:</span><span class="sxs-lookup"><span data-stu-id="bd733-173">For example, by adding **Client App** field to your list, you also get another filter option that enables you to set the following filters:</span></span>

- <span data-ttu-id="bd733-174">Browser</span><span class="sxs-lookup"><span data-stu-id="bd733-174">Browser</span></span>      
- <span data-ttu-id="bd733-175">Exchange ActiveSync (supported)</span><span class="sxs-lookup"><span data-stu-id="bd733-175">Exchange ActiveSync (supported)</span></span>               
- <span data-ttu-id="bd733-176">Exchange ActiveSync (unsupported)</span><span class="sxs-lookup"><span data-stu-id="bd733-176">Exchange ActiveSync (unsupported)</span></span>
- <span data-ttu-id="bd733-177">Other clients</span><span class="sxs-lookup"><span data-stu-id="bd733-177">Other clients</span></span>               
    - <span data-ttu-id="bd733-178">IMAP</span><span class="sxs-lookup"><span data-stu-id="bd733-178">IMAP</span></span>
    - <span data-ttu-id="bd733-179">MAPI</span><span class="sxs-lookup"><span data-stu-id="bd733-179">MAPI</span></span>
    - <span data-ttu-id="bd733-180">Older Office clients</span><span class="sxs-lookup"><span data-stu-id="bd733-180">Older Office clients</span></span>
    - <span data-ttu-id="bd733-181">POP</span><span class="sxs-lookup"><span data-stu-id="bd733-181">POP</span></span>
    - <span data-ttu-id="bd733-182">SMTP</span><span class="sxs-lookup"><span data-stu-id="bd733-182">SMTP</span></span>


<span data-ttu-id="bd733-183">![Sign-in activity](./media/concept-sign-ins/12.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-183">![Sign-in activity](./media/concept-sign-ins/12.png "Sign-in activity")</span></span>


## <a name="download-sign-in-activities"></a><span data-ttu-id="bd733-184">Download sign-in activities</span><span class="sxs-lookup"><span data-stu-id="bd733-184">Download sign-in activities</span></span>

<span data-ttu-id="bd733-185">You can download the sign-in activities data if you want work with it outside the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bd733-185">You can download the sign-in activities data if you want work with it outside the Azure portal.</span></span> <span data-ttu-id="bd733-186">Clicking **Download** creates a CSV file of the most recent 5K records.</span><span class="sxs-lookup"><span data-stu-id="bd733-186">Clicking **Download** creates a CSV file of the most recent 5K records.</span></span>  <span data-ttu-id="bd733-187">In addition to a download button, the Azure portal also provides you with an option to generate a script to download your data.</span><span class="sxs-lookup"><span data-stu-id="bd733-187">In addition to a download button, the Azure portal also provides you with an option to generate a script to download your data.</span></span>  

<span data-ttu-id="bd733-188">![Download](./media/concept-sign-ins/71.png "Download")</span><span class="sxs-lookup"><span data-stu-id="bd733-188">![Download](./media/concept-sign-ins/71.png "Download")</span></span>

<span data-ttu-id="bd733-189">If you need more flexibility, you can use the script solution.</span><span class="sxs-lookup"><span data-stu-id="bd733-189">If you need more flexibility, you can use the script solution.</span></span> <span data-ttu-id="bd733-190">Clicking **Script** creates a PowerShell script that includes all the filters you have set.</span><span class="sxs-lookup"><span data-stu-id="bd733-190">Clicking **Script** creates a PowerShell script that includes all the filters you have set.</span></span> <span data-ttu-id="bd733-191">Download and run this script in **administrator mode** to generate the CSV file.</span><span class="sxs-lookup"><span data-stu-id="bd733-191">Download and run this script in **administrator mode** to generate the CSV file.</span></span> 

### <a name="running-the-script-on-a-windows-10-machine"></a><span data-ttu-id="bd733-192">Running the script on a Windows 10 machine</span><span class="sxs-lookup"><span data-stu-id="bd733-192">Running the script on a Windows 10 machine</span></span>

<span data-ttu-id="bd733-193">If you want to run the script on a **Windows 10** machine, you need to perform a few additional steps first.</span><span class="sxs-lookup"><span data-stu-id="bd733-193">If you want to run the script on a **Windows 10** machine, you need to perform a few additional steps first.</span></span> 

1. <span data-ttu-id="bd733-194">Install the [AzureRM module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.4.0l).</span><span class="sxs-lookup"><span data-stu-id="bd733-194">Install the [AzureRM module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.4.0l).</span></span>
2. <span data-ttu-id="bd733-195">Import the module by opening a PowerShell prompt and running the command **Import-Module AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="bd733-195">Import the module by opening a PowerShell prompt and running the command **Import-Module AzureRM**.</span></span>
3. <span data-ttu-id="bd733-196">Run **Set-ExecutionPolicy unrestricted** and choose **Yes to All**.</span><span class="sxs-lookup"><span data-stu-id="bd733-196">Run **Set-ExecutionPolicy unrestricted** and choose **Yes to All**.</span></span> 
4. <span data-ttu-id="bd733-197">Now you can run the downloaded PowerShell script in administrator mode to generate the CSV file.</span><span class="sxs-lookup"><span data-stu-id="bd733-197">Now you can run the downloaded PowerShell script in administrator mode to generate the CSV file.</span></span>

<span data-ttu-id="bd733-198">In addition to the technical implementation, the number of records you can download is also constrained by the [Azure Active Directory report retention policies](reference-reports-data-retention.md).</span><span class="sxs-lookup"><span data-stu-id="bd733-198">In addition to the technical implementation, the number of records you can download is also constrained by the [Azure Active Directory report retention policies](reference-reports-data-retention.md).</span></span>  


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="bd733-199">Sign-in activities shortcuts</span><span class="sxs-lookup"><span data-stu-id="bd733-199">Sign-in activities shortcuts</span></span>

<span data-ttu-id="bd733-200">In addition to Azure Active Directory, the Azure portal provides you with additional entry points to sign-in activities data:</span><span class="sxs-lookup"><span data-stu-id="bd733-200">In addition to Azure Active Directory, the Azure portal provides you with additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="bd733-201">The identity security protection overview</span><span class="sxs-lookup"><span data-stu-id="bd733-201">The identity security protection overview</span></span>
- <span data-ttu-id="bd733-202">Users</span><span class="sxs-lookup"><span data-stu-id="bd733-202">Users</span></span>
- <span data-ttu-id="bd733-203">Groups</span><span class="sxs-lookup"><span data-stu-id="bd733-203">Groups</span></span>
- <span data-ttu-id="bd733-204">Enterprise applications</span><span class="sxs-lookup"><span data-stu-id="bd733-204">Enterprise applications</span></span>


### <a name="users-sign-ins-activities"></a><span data-ttu-id="bd733-205">Users sign-ins activities</span><span class="sxs-lookup"><span data-stu-id="bd733-205">Users sign-ins activities</span></span>

<span data-ttu-id="bd733-206">With the information provided by the user sign-in report, you find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="bd733-206">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="bd733-207">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="bd733-207">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="bd733-208">How many users have users signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="bd733-208">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="bd733-209">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="bd733-209">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="bd733-210">Your entry point to this data is the user sign-in graph on the **identity security protection** overview page.</span><span class="sxs-lookup"><span data-stu-id="bd733-210">Your entry point to this data is the user sign-in graph on the **identity security protection** overview page.</span></span> <span data-ttu-id="bd733-211">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span><span class="sxs-lookup"><span data-stu-id="bd733-211">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="bd733-212">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="bd733-212">The default for the time period is 30 days.</span></span>

<span data-ttu-id="bd733-213">![Sign-in activity](./media/concept-sign-ins/06.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-213">![Sign-in activity](./media/concept-sign-ins/06.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-214">When you click on a day in the sign-in graph, you get an overview of the sign-in activities for this day.</span><span class="sxs-lookup"><span data-stu-id="bd733-214">When you click on a day in the sign-in graph, you get an overview of the sign-in activities for this day.</span></span>

<span data-ttu-id="bd733-215">Each row in the sign-in activities list shows:</span><span class="sxs-lookup"><span data-stu-id="bd733-215">Each row in the sign-in activities list shows:</span></span>

* <span data-ttu-id="bd733-216">Who has signed in?</span><span class="sxs-lookup"><span data-stu-id="bd733-216">Who has signed in?</span></span>
* <span data-ttu-id="bd733-217">What application was the target of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="bd733-217">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="bd733-218">What is the status of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="bd733-218">What is the status of the sign-in?</span></span>
* <span data-ttu-id="bd733-219">What is the MFA status of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="bd733-219">What is the MFA status of the sign-in?</span></span>

<span data-ttu-id="bd733-220">By clicking an item, you get more details about the sign-in operation:</span><span class="sxs-lookup"><span data-stu-id="bd733-220">By clicking an item, you get more details about the sign-in operation:</span></span>

- <span data-ttu-id="bd733-221">User ID</span><span class="sxs-lookup"><span data-stu-id="bd733-221">User ID</span></span>
- <span data-ttu-id="bd733-222">User</span><span class="sxs-lookup"><span data-stu-id="bd733-222">User</span></span>
- <span data-ttu-id="bd733-223">Username</span><span class="sxs-lookup"><span data-stu-id="bd733-223">Username</span></span>
- <span data-ttu-id="bd733-224">Application ID</span><span class="sxs-lookup"><span data-stu-id="bd733-224">Application ID</span></span>
- <span data-ttu-id="bd733-225">Application</span><span class="sxs-lookup"><span data-stu-id="bd733-225">Application</span></span>
- <span data-ttu-id="bd733-226">Client</span><span class="sxs-lookup"><span data-stu-id="bd733-226">Client</span></span>
- <span data-ttu-id="bd733-227">Location</span><span class="sxs-lookup"><span data-stu-id="bd733-227">Location</span></span>
- <span data-ttu-id="bd733-228">IP address</span><span class="sxs-lookup"><span data-stu-id="bd733-228">IP address</span></span>
- <span data-ttu-id="bd733-229">Date</span><span class="sxs-lookup"><span data-stu-id="bd733-229">Date</span></span>
- <span data-ttu-id="bd733-230">MFA Required</span><span class="sxs-lookup"><span data-stu-id="bd733-230">MFA Required</span></span>
- <span data-ttu-id="bd733-231">Sign-in status</span><span class="sxs-lookup"><span data-stu-id="bd733-231">Sign-in status</span></span>

 
<span data-ttu-id="bd733-232">On the **Users** page, you get a complete overview of all user sign-ins by clicking **Sign-ins** in the **Activity** section.</span><span class="sxs-lookup"><span data-stu-id="bd733-232">On the **Users** page, you get a complete overview of all user sign-ins by clicking **Sign-ins** in the **Activity** section.</span></span>

<span data-ttu-id="bd733-233">![Sign-in activity](./media/concept-sign-ins/08.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-233">![Sign-in activity](./media/concept-sign-ins/08.png "Sign-in activity")</span></span>

## <a name="usage-of-managed-applications"></a><span data-ttu-id="bd733-234">Usage of managed applications</span><span class="sxs-lookup"><span data-stu-id="bd733-234">Usage of managed applications</span></span>

<span data-ttu-id="bd733-235">With an application-centric view of your sign-in data, you can answer questions such as:</span><span class="sxs-lookup"><span data-stu-id="bd733-235">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="bd733-236">Who is using my applications?</span><span class="sxs-lookup"><span data-stu-id="bd733-236">Who is using my applications?</span></span>
* <span data-ttu-id="bd733-237">What are the top 3 applications in your organization?</span><span class="sxs-lookup"><span data-stu-id="bd733-237">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="bd733-238">I have recently rolled out an application.</span><span class="sxs-lookup"><span data-stu-id="bd733-238">I have recently rolled out an application.</span></span> <span data-ttu-id="bd733-239">How is it doing?</span><span class="sxs-lookup"><span data-stu-id="bd733-239">How is it doing?</span></span>

<span data-ttu-id="bd733-240">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bd733-240">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="bd733-241">![Sign-in activity](./media/concept-sign-ins/10.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-241">![Sign-in activity](./media/concept-sign-ins/10.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-242">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span><span class="sxs-lookup"><span data-stu-id="bd733-242">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="bd733-243">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="bd733-243">The default for the time period is 30 days.</span></span>

<span data-ttu-id="bd733-244">![Sign-in activity](./media/concept-sign-ins/47.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-244">![Sign-in activity](./media/concept-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="bd733-245">If you want to, you can set the focus on a specific application.</span><span class="sxs-lookup"><span data-stu-id="bd733-245">If you want to, you can set the focus on a specific application.</span></span>

<span data-ttu-id="bd733-246">![Reporting](./media/concept-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="bd733-246">![Reporting](./media/concept-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="bd733-247">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="bd733-247">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>

<span data-ttu-id="bd733-248">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span><span class="sxs-lookup"><span data-stu-id="bd733-248">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="bd733-249">![Sign-in activity](./media/concept-sign-ins/11.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="bd733-249">![Sign-in activity](./media/concept-sign-ins/11.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="bd733-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd733-250">Next steps</span></span>

<span data-ttu-id="bd733-251">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](reference-sign-ins-error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bd733-251">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](reference-sign-ins-error-codes.md).</span></span>

