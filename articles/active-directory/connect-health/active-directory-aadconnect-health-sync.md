---
title: Using Azure AD Connect Health with sync | Microsoft Docs
description: This is the Azure AD Connect Health page that will discuss how to monitor Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: zhiweiw
manager: mtillman
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0407726fa7dd5801081549f30207eac0b5e46b6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789417"
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="eac84-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="eac84-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="eac84-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="eac84-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="eac84-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span><span class="sxs-lookup"><span data-stu-id="eac84-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="eac84-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span><span class="sxs-lookup"><span data-stu-id="eac84-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![Azure AD Connect Health for Sync](./media/active-directory-aadconnect-health-sync/syncsnapshot.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="eac84-108">Alerts for Azure AD Connect Health for sync</span><span class="sxs-lookup"><span data-stu-id="eac84-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="eac84-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span><span class="sxs-lookup"><span data-stu-id="eac84-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span></span> <span data-ttu-id="eac84-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span><span class="sxs-lookup"><span data-stu-id="eac84-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span></span> <span data-ttu-id="eac84-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span><span class="sxs-lookup"><span data-stu-id="eac84-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span></span> <span data-ttu-id="eac84-112">You can also view historical data on alerts that were resolved in the past.</span><span class="sxs-lookup"><span data-stu-id="eac84-112">You can also view historical data on alerts that were resolved in the past.</span></span>

<span data-ttu-id="eac84-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span><span class="sxs-lookup"><span data-stu-id="eac84-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span></span>

![Azure AD Connect sync error](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="eac84-115">Limited Evaluation of Alerts</span><span class="sxs-lookup"><span data-stu-id="eac84-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="eac84-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="eac84-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span></span>

<span data-ttu-id="eac84-117">This limits the evaluation of alerts by the service.</span><span class="sxs-lookup"><span data-stu-id="eac84-117">This limits the evaluation of alerts by the service.</span></span> <span data-ttu-id="eac84-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span><span class="sxs-lookup"><span data-stu-id="eac84-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span></span>

![Azure AD Connect Health for Sync](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="eac84-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span><span class="sxs-lookup"><span data-stu-id="eac84-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span></span>

![Azure AD Connect Health for Sync](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="eac84-122">Sync Insight</span><span class="sxs-lookup"><span data-stu-id="eac84-122">Sync Insight</span></span>
<span data-ttu-id="eac84-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span><span class="sxs-lookup"><span data-stu-id="eac84-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span></span> <span data-ttu-id="eac84-124">This feature provides an easy way to visualize this using the below graphs:</span><span class="sxs-lookup"><span data-stu-id="eac84-124">This feature provides an easy way to visualize this using the below graphs:</span></span>   

* <span data-ttu-id="eac84-125">Latency of sync operations</span><span class="sxs-lookup"><span data-stu-id="eac84-125">Latency of sync operations</span></span>
* <span data-ttu-id="eac84-126">Object Change trend</span><span class="sxs-lookup"><span data-stu-id="eac84-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="eac84-127">Sync Latency</span><span class="sxs-lookup"><span data-stu-id="eac84-127">Sync Latency</span></span>
<span data-ttu-id="eac84-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span><span class="sxs-lookup"><span data-stu-id="eac84-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="eac84-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span><span class="sxs-lookup"><span data-stu-id="eac84-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span></span>

![Sync Latency](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="eac84-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span><span class="sxs-lookup"><span data-stu-id="eac84-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span></span>  <span data-ttu-id="eac84-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span><span class="sxs-lookup"><span data-stu-id="eac84-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="eac84-133">Sync Object Changes</span><span class="sxs-lookup"><span data-stu-id="eac84-133">Sync Object Changes</span></span>
<span data-ttu-id="eac84-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eac84-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span></span>  <span data-ttu-id="eac84-135">Today, trying to gather this information from the sync logs is difficult.</span><span class="sxs-lookup"><span data-stu-id="eac84-135">Today, trying to gather this information from the sync logs is difficult.</span></span>  <span data-ttu-id="eac84-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span><span class="sxs-lookup"><span data-stu-id="eac84-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span></span>

![Sync Latency](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="eac84-138">Object Level Synchronization Error Report (Preview)</span><span class="sxs-lookup"><span data-stu-id="eac84-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="eac84-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="eac84-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="eac84-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span><span class="sxs-lookup"><span data-stu-id="eac84-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="eac84-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span><span class="sxs-lookup"><span data-stu-id="eac84-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span></span> <span data-ttu-id="eac84-142">("Export" on the Azure AD Connector.)</span><span class="sxs-lookup"><span data-stu-id="eac84-142">("Export" on the Azure AD Connector.)</span></span>
* <span data-ttu-id="eac84-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span><span class="sxs-lookup"><span data-stu-id="eac84-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span></span>
* <span data-ttu-id="eac84-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync. It provides the following key capabilities</span><span class="sxs-lookup"><span data-stu-id="eac84-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync. It provides the following key capabilities</span></span>

  * <span data-ttu-id="eac84-145">Categorization of errors</span><span class="sxs-lookup"><span data-stu-id="eac84-145">Categorization of errors</span></span>
  * <span data-ttu-id="eac84-146">List of objects with error per category</span><span class="sxs-lookup"><span data-stu-id="eac84-146">List of objects with error per category</span></span>
  * <span data-ttu-id="eac84-147">All the data about the errors at one place</span><span class="sxs-lookup"><span data-stu-id="eac84-147">All the data about the errors at one place</span></span>
  * <span data-ttu-id="eac84-148">Side by side comparison of Objects with error due to a conflict</span><span class="sxs-lookup"><span data-stu-id="eac84-148">Side by side comparison of Objects with error due to a conflict</span></span>
  * <span data-ttu-id="eac84-149">Download the error report as a CVS (coming soon)</span><span class="sxs-lookup"><span data-stu-id="eac84-149">Download the error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="eac84-150">Categorization of Errors</span><span class="sxs-lookup"><span data-stu-id="eac84-150">Categorization of Errors</span></span>
<span data-ttu-id="eac84-151">The report categorizes the existing synchronization errors in the following categories:</span><span class="sxs-lookup"><span data-stu-id="eac84-151">The report categorizes the existing synchronization errors in the following categories:</span></span>

| <span data-ttu-id="eac84-152">Category</span><span class="sxs-lookup"><span data-stu-id="eac84-152">Category</span></span> | <span data-ttu-id="eac84-153">Description</span><span class="sxs-lookup"><span data-stu-id="eac84-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eac84-154">Duplicate Attribute</span><span class="sxs-lookup"><span data-stu-id="eac84-154">Duplicate Attribute</span></span> |<span data-ttu-id="eac84-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="eac84-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="eac84-156">Data Mismatch</span><span class="sxs-lookup"><span data-stu-id="eac84-156">Data Mismatch</span></span> |<span data-ttu-id="eac84-157">Errors when the soft-match fails to match objects that result in synchronization errors.</span><span class="sxs-lookup"><span data-stu-id="eac84-157">Errors when the soft-match fails to match objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="eac84-158">Data Validation Failure</span><span class="sxs-lookup"><span data-stu-id="eac84-158">Data Validation Failure</span></span> |<span data-ttu-id="eac84-159">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eac84-159">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="eac84-160">Federated Domain Change</span><span class="sxs-lookup"><span data-stu-id="eac84-160">Federated Domain Change</span></span> | <span data-ttu-id="eac84-161">Errors when accounts use a different federated domain.</span><span class="sxs-lookup"><span data-stu-id="eac84-161">Errors when accounts use a different federated domain.</span></span> |
| <span data-ttu-id="eac84-162">Large Attribute</span><span class="sxs-lookup"><span data-stu-id="eac84-162">Large Attribute</span></span> |<span data-ttu-id="eac84-163">Errors when one or more attributes are larger than the allowed size, length or count.</span><span class="sxs-lookup"><span data-stu-id="eac84-163">Errors when one or more attributes are larger than the allowed size, length or count.</span></span> |
| <span data-ttu-id="eac84-164">Other</span><span class="sxs-lookup"><span data-stu-id="eac84-164">Other</span></span> |<span data-ttu-id="eac84-165">All other errors that don't fit in the above categories.</span><span class="sxs-lookup"><span data-stu-id="eac84-165">All other errors that don't fit in the above categories.</span></span> <span data-ttu-id="eac84-166">Based on feedback, this category will be split in sub categories.</span><span class="sxs-lookup"><span data-stu-id="eac84-166">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="eac84-167">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/SyncErrorByTypes.PNG)</span><span class="sxs-lookup"><span data-stu-id="eac84-167">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/SyncErrorByTypes.PNG)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="eac84-168">List of objects with error per category</span><span class="sxs-lookup"><span data-stu-id="eac84-168">List of objects with error per category</span></span>
<span data-ttu-id="eac84-169">Drilling into each category will provide the list of objects having the error in that category.</span><span class="sxs-lookup"><span data-stu-id="eac84-169">Drilling into each category will provide the list of objects having the error in that category.</span></span>
<span data-ttu-id="eac84-170">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="eac84-170">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="eac84-171">Error Details</span><span class="sxs-lookup"><span data-stu-id="eac84-171">Error Details</span></span>
<span data-ttu-id="eac84-172">Following data is available in the detailed view for each error</span><span class="sxs-lookup"><span data-stu-id="eac84-172">Following data is available in the detailed view for each error</span></span>

* <span data-ttu-id="eac84-173">Highlighted conflicting attribute</span><span class="sxs-lookup"><span data-stu-id="eac84-173">Highlighted conflicting attribute</span></span>
* <span data-ttu-id="eac84-174">Identifiers for the *AD Object* involved</span><span class="sxs-lookup"><span data-stu-id="eac84-174">Identifiers for the *AD Object* involved</span></span>
* <span data-ttu-id="eac84-175">Identifiers for the *Azure AD Object* involved (as applicable)</span><span class="sxs-lookup"><span data-stu-id="eac84-175">Identifiers for the *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="eac84-176">Error description and how to fix</span><span class="sxs-lookup"><span data-stu-id="eac84-176">Error description and how to fix</span></span>

![Sync Error Report Details](./media/active-directory-aadconnect-health-sync/duplicateAttributeSyncError.png)

### <a name="download-the-error-report-as-csv"></a><span data-ttu-id="eac84-178">Download the error report as CSV</span><span class="sxs-lookup"><span data-stu-id="eac84-178">Download the error report as CSV</span></span>
<span data-ttu-id="eac84-179">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span><span class="sxs-lookup"><span data-stu-id="eac84-179">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span></span>

### <a name="diagnose-and-remediate-sync-errors"></a><span data-ttu-id="eac84-180">Diagnose and remediate sync errors</span><span class="sxs-lookup"><span data-stu-id="eac84-180">Diagnose and remediate sync errors</span></span> 
<span data-ttu-id="eac84-181">For specific duplicated attribute sync error scenario involving user Source Anchor update, you can fix them directly from the portal.</span><span class="sxs-lookup"><span data-stu-id="eac84-181">For specific duplicated attribute sync error scenario involving user Source Anchor update, you can fix them directly from the portal.</span></span> <span data-ttu-id="eac84-182">Read more about [Diagnose and remediate duplicated attribute sync errors](active-directory-aadconnect-health-diagnose-sync-errors.md)</span><span class="sxs-lookup"><span data-stu-id="eac84-182">Read more about [Diagnose and remediate duplicated attribute sync errors](active-directory-aadconnect-health-diagnose-sync-errors.md)</span></span>

## <a name="related-links"></a><span data-ttu-id="eac84-183">Related links</span><span class="sxs-lookup"><span data-stu-id="eac84-183">Related links</span></span>
* [<span data-ttu-id="eac84-184">Troubleshooting Errors during synchronization</span><span class="sxs-lookup"><span data-stu-id="eac84-184">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="eac84-185">Duplicate Attribute Resiliency</span><span class="sxs-lookup"><span data-stu-id="eac84-185">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="eac84-186">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="eac84-186">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="eac84-187">Azure AD Connect Health Agent Installation</span><span class="sxs-lookup"><span data-stu-id="eac84-187">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="eac84-188">Azure AD Connect Health Operations</span><span class="sxs-lookup"><span data-stu-id="eac84-188">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="eac84-189">Using Azure AD Connect Health with AD FS</span><span class="sxs-lookup"><span data-stu-id="eac84-189">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="eac84-190">Using Azure AD Connect Health with AD DS</span><span class="sxs-lookup"><span data-stu-id="eac84-190">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="eac84-191">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="eac84-191">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="eac84-192">Azure AD Connect Health Version History</span><span class="sxs-lookup"><span data-stu-id="eac84-192">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)
