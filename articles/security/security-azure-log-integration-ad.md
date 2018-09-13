---
title: Azure Log Integration (AZLOG) with Active directory audit logs | Microsoft Docs
description: Learn how to install the Azure log integration service and integrate logs from Azure audit logs
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: ''
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: f7c2f702a4ff2af8bb7487d49f5c6f9bf5199a49
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564226"
---
#<a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3b503-103">Integrate Azure Active Directory Audit logs</span><span class="sxs-lookup"><span data-stu-id="3b503-103">Integrate Azure Active Directory Audit logs</span></span>

<span data-ttu-id="3b503-104">Azure Active directory audit events help you identify privileged actions that occurred in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b503-104">Azure Active directory audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="3b503-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)</span><span class="sxs-lookup"><span data-stu-id="3b503-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)</span></span>

>[!NOTE]
<span data-ttu-id="3b503-106">You must have successfully completed the steps in the [Get started](security-azure-log-integration-get-started.md) article before performing the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="3b503-106">You must have successfully completed the steps in the [Get started](security-azure-log-integration-get-started.md) article before performing the steps in this article.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3b503-107">Steps to integrate Azure Active directory audit logs</span><span class="sxs-lookup"><span data-stu-id="3b503-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="3b503-108">Open the command prompt and cd into **c:\Program Files\Microsoft Azure Log Integration**</span><span class="sxs-lookup"><span data-stu-id="3b503-108">Open the command prompt and cd into **c:\Program Files\Microsoft Azure Log Integration**</span></span>
2. <span data-ttu-id="3b503-109">Run the command:</span><span class="sxs-lookup"><span data-stu-id="3b503-109">Run the command:</span></span>

 ``azlog createazureid``
 
 <span data-ttu-id="3b503-110">This command prompts you for your Azure login.</span><span class="sxs-lookup"><span data-stu-id="3b503-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="3b503-111">The command then creates an Azure Active Directory Service Principal in the Azure AD Tenants that host the Azure subscriptions in which the logged in user is an Administrator, a Co-Administrator, or an Owner.</span><span class="sxs-lookup"><span data-stu-id="3b503-111">The command then creates an Azure Active Directory Service Principal in the Azure AD Tenants that host the Azure subscriptions in which the logged in user is an Administrator, a Co-Administrator, or an Owner.</span></span> <span data-ttu-id="3b503-112">The command will fail if the logged in user is only a Guest user in the Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="3b503-112">The command will fail if the logged in user is only a Guest user in the Azure AD Tenant.</span></span> <span data-ttu-id="3b503-113">Authentication to Azure is done through Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="3b503-113">Authentication to Azure is done through Azure Active Directory (AD).</span></span> <span data-ttu-id="3b503-114">Creating a service principal for Azlog Integration creates the Azure AD identity that will be given access to read from Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3b503-114">Creating a service principal for Azlog Integration creates the Azure AD identity that will be given access to read from Azure subscriptions.</span></span>
 
3. <span data-ttu-id="3b503-115">Run the command providing your tenantID.</span><span class="sxs-lookup"><span data-stu-id="3b503-115">Run the command providing your tenantID.</span></span> <span data-ttu-id="3b503-116">You will need to be member of the tenant admin role to run the command.</span><span class="sxs-lookup"><span data-stu-id="3b503-116">You will need to be member of the tenant admin role to run the command.</span></span>

``Azlog.exe authorizedirectoryreader tenantId``

<span data-ttu-id="3b503-117">Example</span><span class="sxs-lookup"><span data-stu-id="3b503-117">Example</span></span>

``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

<span data-ttu-id="3b503-118">Check the following folders to confirm that the Azure Active Directory Audit log JSON files are created in:</span><span class="sxs-lookup"><span data-stu-id="3b503-118">Check the following folders to confirm that the Azure Active Directory Audit log JSON files are created in:</span></span>

* <span data-ttu-id="3b503-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="3b503-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
* <span data-ttu-id="3b503-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="3b503-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="3b503-121">Point the standard SIEM file forwarder connector to the appropriate folder to pipe the data to the SIEM instance.</span><span class="sxs-lookup"><span data-stu-id="3b503-121">Point the standard SIEM file forwarder connector to the appropriate folder to pipe the data to the SIEM instance.</span></span> <span data-ttu-id="3b503-122">You may need some field mappings based on the SIEM product you are using.</span><span class="sxs-lookup"><span data-stu-id="3b503-122">You may need some field mappings based on the SIEM product you are using.</span></span>

<span data-ttu-id="3b503-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="3b503-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="3b503-124">This forum provides the AzLog community the ability support each other with questions, answers, tips, and tricks on how to get the most out of Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="3b503-124">This forum provides the AzLog community the ability support each other with questions, answers, tips, and tricks on how to get the most out of Azure Log Integration.</span></span> <span data-ttu-id="3b503-125">In addition, the Azure Log Integration team monitors this forum and will help whenever we can.</span><span class="sxs-lookup"><span data-stu-id="3b503-125">In addition, the Azure Log Integration team monitors this forum and will help whenever we can.</span></span> 

<span data-ttu-id="3b503-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="3b503-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="3b503-127">To do this, select **Log Integration** as the service for which you are requesting support.</span><span class="sxs-lookup"><span data-stu-id="3b503-127">To do this, select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b503-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b503-128">Next steps</span></span>
<span data-ttu-id="3b503-129">To learn more about Azure Log Integration, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="3b503-129">To learn more about Azure Log Integration, see the following documents:</span></span>

* <span data-ttu-id="3b503-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span><span class="sxs-lookup"><span data-stu-id="3b503-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span></span>
* <span data-ttu-id="3b503-131">[Introduction to Azure log integration](security-azure-log-integration-overview.md) – This document introduces you to Azure log integration, its key capabilities, and how it works.</span><span class="sxs-lookup"><span data-stu-id="3b503-131">[Introduction to Azure log integration](security-azure-log-integration-overview.md) – This document introduces you to Azure log integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="3b503-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how to configure Azure log integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="3b503-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how to configure Azure log integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="3b503-133">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span><span class="sxs-lookup"><span data-stu-id="3b503-133">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span></span>
* <span data-ttu-id="3b503-134">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure Audit Logs, with your log analytics or SIEM solution.</span><span class="sxs-lookup"><span data-stu-id="3b503-134">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure Audit Logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="3b503-135">[New features for Azure diagnostics and Azure Audit Logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – This blog post introduces you to Azure Audit Logs and other features that help you gain insights into the operations of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3b503-135">[New features for Azure diagnostics and Azure Audit Logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – This blog post introduces you to Azure Audit Logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
