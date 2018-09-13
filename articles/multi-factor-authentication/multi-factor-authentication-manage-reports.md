---
title: View access reports for Azure MFA in the cloud | Microsoft Docs
description: This describes how to use the Azure Multi-Factor Authentication feature - reports.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: kgremban
ms.openlocfilehash: 3e3765efb1a65dfb52cc004d2bfc03ab95795ced
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556003"
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="43b6c-103">Reports in Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="43b6c-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="43b6c-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span><span class="sxs-lookup"><span data-stu-id="43b6c-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="43b6c-105">These reports can be accessed through the Multi-Factor Authentication Management Portal, which requires that you have an Azure MFA Provider, or an Azure MFA, Azure AD Premium or Enterprise Mobility Suite license.</span><span class="sxs-lookup"><span data-stu-id="43b6c-105">These reports can be accessed through the Multi-Factor Authentication Management Portal, which requires that you have an Azure MFA Provider, or an Azure MFA, Azure AD Premium or Enterprise Mobility Suite license.</span></span> <span data-ttu-id="43b6c-106">The following is a list of the available reports.</span><span class="sxs-lookup"><span data-stu-id="43b6c-106">The following is a list of the available reports.</span></span>

<span data-ttu-id="43b6c-107">You can access reports through the Azure Management portal.</span><span class="sxs-lookup"><span data-stu-id="43b6c-107">You can access reports through the Azure Management portal.</span></span>

| <span data-ttu-id="43b6c-108">Name</span><span class="sxs-lookup"><span data-stu-id="43b6c-108">Name</span></span> | <span data-ttu-id="43b6c-109">Description</span><span class="sxs-lookup"><span data-stu-id="43b6c-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="43b6c-110">Usage</span><span class="sxs-lookup"><span data-stu-id="43b6c-110">Usage</span></span> |<span data-ttu-id="43b6c-111">The usage reports display information on overall usage, user summary and user details.</span><span class="sxs-lookup"><span data-stu-id="43b6c-111">The usage reports display information on overall usage, user summary and user details.</span></span> |
| <span data-ttu-id="43b6c-112">Server Status</span><span class="sxs-lookup"><span data-stu-id="43b6c-112">Server Status</span></span> |<span data-ttu-id="43b6c-113">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span><span class="sxs-lookup"><span data-stu-id="43b6c-113">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="43b6c-114">Blocked User History</span><span class="sxs-lookup"><span data-stu-id="43b6c-114">Blocked User History</span></span> |<span data-ttu-id="43b6c-115">These reports show the history of requests to block or unblock users.</span><span class="sxs-lookup"><span data-stu-id="43b6c-115">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="43b6c-116">Bypassed User History</span><span class="sxs-lookup"><span data-stu-id="43b6c-116">Bypassed User History</span></span> |<span data-ttu-id="43b6c-117">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span><span class="sxs-lookup"><span data-stu-id="43b6c-117">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="43b6c-118">Fraud Alert</span><span class="sxs-lookup"><span data-stu-id="43b6c-118">Fraud Alert</span></span> |<span data-ttu-id="43b6c-119">Shows a history of fraud alerts submitted during the date range you specified.</span><span class="sxs-lookup"><span data-stu-id="43b6c-119">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="43b6c-120">Queued</span><span class="sxs-lookup"><span data-stu-id="43b6c-120">Queued</span></span> |<span data-ttu-id="43b6c-121">Lists reports queued for processing and their status.</span><span class="sxs-lookup"><span data-stu-id="43b6c-121">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="43b6c-122">A link to download or view the report is provided when the report is complete.</span><span class="sxs-lookup"><span data-stu-id="43b6c-122">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="to-view-reports"></a><span data-ttu-id="43b6c-123">To view reports</span><span class="sxs-lookup"><span data-stu-id="43b6c-123">To view reports</span></span>
1. <span data-ttu-id="43b6c-124">Log on to http://azure.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="43b6c-124">Log on to http://azure.microsoft.com</span></span>
2. <span data-ttu-id="43b6c-125">On the left, select Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43b6c-125">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="43b6c-126">Select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="43b6c-126">Select one of the following options:</span></span>
   * <span data-ttu-id="43b6c-127">**Option 1**: Click the Multi-Factor Auth Providers tab. Select your MFA provider and click the Manage button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="43b6c-127">**Option 1**: Click the Multi-Factor Auth Providers tab. Select your MFA provider and click the Manage button at the bottom.</span></span>
   * <span data-ttu-id="43b6c-128">**Option 2**: Select your directory and click the Configure tab. Under the multi-factor authentication section, select Manage service settings.</span><span class="sxs-lookup"><span data-stu-id="43b6c-128">**Option 2**: Select your directory and click the Configure tab. Under the multi-factor authentication section, select Manage service settings.</span></span> <span data-ttu-id="43b6c-129">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span><span class="sxs-lookup"><span data-stu-id="43b6c-129">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="43b6c-130">In the Azure Multi-Factor Authentication Management Portal, you will see the View a Report section in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="43b6c-130">In the Azure Multi-Factor Authentication Management Portal, you will see the View a Report section in the left navigation.</span></span> <span data-ttu-id="43b6c-131">From here you can select the reports described above.</span><span class="sxs-lookup"><span data-stu-id="43b6c-131">From here you can select the reports described above.</span></span>

<span data-ttu-id="43b6c-132"><center>![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="43b6c-132"><center>![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="43b6c-133">**Additional Resources**</span><span class="sxs-lookup"><span data-stu-id="43b6c-133">**Additional Resources**</span></span>

* [<span data-ttu-id="43b6c-134">For Users</span><span class="sxs-lookup"><span data-stu-id="43b6c-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="43b6c-135">Azure Multi-Factor Authentication on MSDN</span><span class="sxs-lookup"><span data-stu-id="43b6c-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)

