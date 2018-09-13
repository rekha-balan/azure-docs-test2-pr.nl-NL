---
title: Using Azure AD Connect Health with sync | Microsoft Docs
description: This is the Azure AD Connect Health page that will discuss how to monitor Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/27/2017
ms.author: vakarand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1845dee149399fe76e307d86cd740b85d2e99974
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554514"
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="40fef-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="40fef-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="40fef-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="40fef-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="40fef-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span><span class="sxs-lookup"><span data-stu-id="40fef-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="40fef-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span><span class="sxs-lookup"><span data-stu-id="40fef-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="40fef-108">Alerts for Azure AD Connect Health for sync</span><span class="sxs-lookup"><span data-stu-id="40fef-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="40fef-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span><span class="sxs-lookup"><span data-stu-id="40fef-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span></span> <span data-ttu-id="40fef-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span><span class="sxs-lookup"><span data-stu-id="40fef-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span></span> <span data-ttu-id="40fef-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span><span class="sxs-lookup"><span data-stu-id="40fef-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span></span> <span data-ttu-id="40fef-112">You can also view historical data on alerts that were resolved in the past.</span><span class="sxs-lookup"><span data-stu-id="40fef-112">You can also view historical data on alerts that were resolved in the past.</span></span>

<span data-ttu-id="40fef-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span><span class="sxs-lookup"><span data-stu-id="40fef-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span></span>

![Azure AD Connect sync error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="40fef-115">Limited Evaluation of Alerts</span><span class="sxs-lookup"><span data-stu-id="40fef-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="40fef-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="40fef-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span></span>

<span data-ttu-id="40fef-117">This limits the evaluation of alerts by the service.</span><span class="sxs-lookup"><span data-stu-id="40fef-117">This limits the evaluation of alerts by the service.</span></span> <span data-ttu-id="40fef-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span><span class="sxs-lookup"><span data-stu-id="40fef-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span></span>

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="40fef-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span><span class="sxs-lookup"><span data-stu-id="40fef-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span></span>

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="40fef-122">Sync Insight</span><span class="sxs-lookup"><span data-stu-id="40fef-122">Sync Insight</span></span>
<span data-ttu-id="40fef-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span><span class="sxs-lookup"><span data-stu-id="40fef-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span></span> <span data-ttu-id="40fef-124">This feature provides an easy way to visualize this using the below graphs:</span><span class="sxs-lookup"><span data-stu-id="40fef-124">This feature provides an easy way to visualize this using the below graphs:</span></span>   

* <span data-ttu-id="40fef-125">Latency of sync operations</span><span class="sxs-lookup"><span data-stu-id="40fef-125">Latency of sync operations</span></span>
* <span data-ttu-id="40fef-126">Object Change trend</span><span class="sxs-lookup"><span data-stu-id="40fef-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="40fef-127">Sync Latency</span><span class="sxs-lookup"><span data-stu-id="40fef-127">Sync Latency</span></span>
<span data-ttu-id="40fef-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span><span class="sxs-lookup"><span data-stu-id="40fef-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="40fef-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span><span class="sxs-lookup"><span data-stu-id="40fef-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span></span>

![Sync Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="40fef-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span><span class="sxs-lookup"><span data-stu-id="40fef-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span></span>  <span data-ttu-id="40fef-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span><span class="sxs-lookup"><span data-stu-id="40fef-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="40fef-133">Sync Object Changes</span><span class="sxs-lookup"><span data-stu-id="40fef-133">Sync Object Changes</span></span>
<span data-ttu-id="40fef-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40fef-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span></span>  <span data-ttu-id="40fef-135">Today, trying to gather this information from the sync logs is difficult.</span><span class="sxs-lookup"><span data-stu-id="40fef-135">Today, trying to gather this information from the sync logs is difficult.</span></span>  <span data-ttu-id="40fef-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span><span class="sxs-lookup"><span data-stu-id="40fef-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span></span>

![Sync Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="40fef-138">Object Level Synchronization Error Report (Preview)</span><span class="sxs-lookup"><span data-stu-id="40fef-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="40fef-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="40fef-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="40fef-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span><span class="sxs-lookup"><span data-stu-id="40fef-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="40fef-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span><span class="sxs-lookup"><span data-stu-id="40fef-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span></span> <span data-ttu-id="40fef-142">("Export" on the Azure AD Connector.)</span><span class="sxs-lookup"><span data-stu-id="40fef-142">("Export" on the Azure AD Connector.)</span></span>
* <span data-ttu-id="40fef-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span><span class="sxs-lookup"><span data-stu-id="40fef-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span></span>
* <span data-ttu-id="40fef-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync. It provides the following key capabilities</span><span class="sxs-lookup"><span data-stu-id="40fef-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync. It provides the following key capabilities</span></span>

  * <span data-ttu-id="40fef-145">Categorization of errors</span><span class="sxs-lookup"><span data-stu-id="40fef-145">Categorization of errors</span></span>
  * <span data-ttu-id="40fef-146">List of objects with error per category</span><span class="sxs-lookup"><span data-stu-id="40fef-146">List of objects with error per category</span></span>
  * <span data-ttu-id="40fef-147">All the data about the errors at one place</span><span class="sxs-lookup"><span data-stu-id="40fef-147">All the data about the errors at one place</span></span>
  * <span data-ttu-id="40fef-148">Side by side comparison of Objects with error due to a conflict</span><span class="sxs-lookup"><span data-stu-id="40fef-148">Side by side comparison of Objects with error due to a conflict</span></span>
  * <span data-ttu-id="40fef-149">Download the error report as a CVS (coming soon)</span><span class="sxs-lookup"><span data-stu-id="40fef-149">Download the error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="40fef-150">Categorization of Errors</span><span class="sxs-lookup"><span data-stu-id="40fef-150">Categorization of Errors</span></span>
<span data-ttu-id="40fef-151">The report categorizes the existing synchronization errors in the following categories:</span><span class="sxs-lookup"><span data-stu-id="40fef-151">The report categorizes the existing synchronization errors in the following categories:</span></span>

| <span data-ttu-id="40fef-152">Category</span><span class="sxs-lookup"><span data-stu-id="40fef-152">Category</span></span> | <span data-ttu-id="40fef-153">Description</span><span class="sxs-lookup"><span data-stu-id="40fef-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40fef-154">Duplicate Attribute</span><span class="sxs-lookup"><span data-stu-id="40fef-154">Duplicate Attribute</span></span> |<span data-ttu-id="40fef-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="40fef-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="40fef-156">Data Mismatch</span><span class="sxs-lookup"><span data-stu-id="40fef-156">Data Mismatch</span></span> |<span data-ttu-id="40fef-157">Errors when the soft-match fails to match objects that result in synchronization errors.</span><span class="sxs-lookup"><span data-stu-id="40fef-157">Errors when the soft-match fails to match objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="40fef-158">Data Validation Failure</span><span class="sxs-lookup"><span data-stu-id="40fef-158">Data Validation Failure</span></span> |<span data-ttu-id="40fef-159">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40fef-159">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="40fef-160">Large Attribute</span><span class="sxs-lookup"><span data-stu-id="40fef-160">Large Attribute</span></span> |<span data-ttu-id="40fef-161">Errors when one or more attributes are larger than the allowed size, length or count.</span><span class="sxs-lookup"><span data-stu-id="40fef-161">Errors when one or more attributes are larger than the allowed size, length or count.</span></span> |
| <span data-ttu-id="40fef-162">Other</span><span class="sxs-lookup"><span data-stu-id="40fef-162">Other</span></span> |<span data-ttu-id="40fef-163">All other errors that don't fit in the above categories.</span><span class="sxs-lookup"><span data-stu-id="40fef-163">All other errors that don't fit in the above categories.</span></span> <span data-ttu-id="40fef-164">Based on feedback, this category will be split in sub categories.</span><span class="sxs-lookup"><span data-stu-id="40fef-164">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="40fef-165">![Sync Error Report Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="40fef-165">![Sync Error Report Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="40fef-166">List of objects with error per category</span><span class="sxs-lookup"><span data-stu-id="40fef-166">List of objects with error per category</span></span>
<span data-ttu-id="40fef-167">Drilling into each category will provide the list of objects having the error in that category.</span><span class="sxs-lookup"><span data-stu-id="40fef-167">Drilling into each category will provide the list of objects having the error in that category.</span></span>
<span data-ttu-id="40fef-168">![Sync Error Report List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="40fef-168">![Sync Error Report List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="40fef-169">Error Details</span><span class="sxs-lookup"><span data-stu-id="40fef-169">Error Details</span></span>
<span data-ttu-id="40fef-170">Following data is available in the detailed view for each error</span><span class="sxs-lookup"><span data-stu-id="40fef-170">Following data is available in the detailed view for each error</span></span>

* <span data-ttu-id="40fef-171">Identifiers for the *AD Object* involved</span><span class="sxs-lookup"><span data-stu-id="40fef-171">Identifiers for the *AD Object* involved</span></span>
* <span data-ttu-id="40fef-172">Identifiers for the *Azure AD Object* involved (as applicable)</span><span class="sxs-lookup"><span data-stu-id="40fef-172">Identifiers for the *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="40fef-173">Error description and how to fix</span><span class="sxs-lookup"><span data-stu-id="40fef-173">Error description and how to fix</span></span>
* <span data-ttu-id="40fef-174">Related articles</span><span class="sxs-lookup"><span data-stu-id="40fef-174">Related articles</span></span>

![Sync Error Report Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a><span data-ttu-id="40fef-176">Download the error report as CSV</span><span class="sxs-lookup"><span data-stu-id="40fef-176">Download the error report as CSV</span></span>
<span data-ttu-id="40fef-177">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span><span class="sxs-lookup"><span data-stu-id="40fef-177">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="40fef-178">Related links</span><span class="sxs-lookup"><span data-stu-id="40fef-178">Related links</span></span>
* [<span data-ttu-id="40fef-179">Troubleshooting Errors during synchronization</span><span class="sxs-lookup"><span data-stu-id="40fef-179">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="40fef-180">Duplicate Attribute Resiliency</span><span class="sxs-lookup"><span data-stu-id="40fef-180">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="40fef-181">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="40fef-181">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="40fef-182">Azure AD Connect Health Agent Installation</span><span class="sxs-lookup"><span data-stu-id="40fef-182">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="40fef-183">Azure AD Connect Health Operations</span><span class="sxs-lookup"><span data-stu-id="40fef-183">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="40fef-184">Using Azure AD Connect Health with AD FS</span><span class="sxs-lookup"><span data-stu-id="40fef-184">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="40fef-185">Using Azure AD Connect Health with AD DS</span><span class="sxs-lookup"><span data-stu-id="40fef-185">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="40fef-186">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="40fef-186">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="40fef-187">Azure AD Connect Health Version History</span><span class="sxs-lookup"><span data-stu-id="40fef-187">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)









