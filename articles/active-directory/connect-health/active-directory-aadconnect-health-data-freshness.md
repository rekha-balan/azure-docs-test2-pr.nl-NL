---
title: Azure AD Connect Health - Health service data is not up to date alert | Microsoft Docs
description: This document describes the cause of "Health service data is not up to date" alert and how to troubleshoot it.
services: active-directory
documentationcenter: ''
author: zhiweiw
manager: maheshu
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2018
ms.author: zhiweiw
ms.openlocfilehash: 45e88320a64770239c8f322212e12ca7826cd0da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856487"
---
# <a name="health-service-data-is-not-up-to-date-alert"></a><span data-ttu-id="89d17-103">Health service data is not up to date alert</span><span class="sxs-lookup"><span data-stu-id="89d17-103">Health service data is not up to date alert</span></span>

## <a name="overview"></a><span data-ttu-id="89d17-104">Overview</span><span class="sxs-lookup"><span data-stu-id="89d17-104">Overview</span></span>
<li><span data-ttu-id="89d17-105">Azure AD Connect Health generates data fresh alert when it does not receive all the data points from the server for two hours.</span><span class="sxs-lookup"><span data-stu-id="89d17-105">Azure AD Connect Health generates data fresh alert when it does not receive all the data points from the server for two hours.</span></span> <span data-ttu-id="89d17-106">The alert title is **Health service data is not up to date**.</span><span class="sxs-lookup"><span data-stu-id="89d17-106">The alert title is **Health service data is not up to date**.</span></span> </li>
<li><span data-ttu-id="89d17-107">The **Warning** status alert fires if Connect Health does not receive partial data elements sent from server for two hours.</span><span class="sxs-lookup"><span data-stu-id="89d17-107">The **Warning** status alert fires if Connect Health does not receive partial data elements sent from server for two hours.</span></span> <span data-ttu-id="89d17-108">Warning status alert does not trigger email notifications to the tenant admin.</span><span class="sxs-lookup"><span data-stu-id="89d17-108">Warning status alert does not trigger email notifications to the tenant admin.</span></span> </li>
<li><span data-ttu-id="89d17-109">The **Error** status alert fires if Connect Health does not receive any data elements sent from server for two hours.</span><span class="sxs-lookup"><span data-stu-id="89d17-109">The **Error** status alert fires if Connect Health does not receive any data elements sent from server for two hours.</span></span> <span data-ttu-id="89d17-110">Error status alert triggers email notifications to the tenant admin.</span><span class="sxs-lookup"><span data-stu-id="89d17-110">Error status alert triggers email notifications to the tenant admin.</span></span> </li>

>[!IMPORTANT] 
> <span data-ttu-id="89d17-111">This alert follows Connect Health [data retention policy](active-directory-aadconnect-health-gdpr.md#data-retention-policy)</span><span class="sxs-lookup"><span data-stu-id="89d17-111">This alert follows Connect Health [data retention policy](active-directory-aadconnect-health-gdpr.md#data-retention-policy)</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="89d17-112">Troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="89d17-112">Troubleshooting steps</span></span> 
* <span data-ttu-id="89d17-113">Make sure to go over and meet the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="89d17-113">Make sure to go over and meet the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements).</span></span>
* <span data-ttu-id="89d17-114">Use [test connectivity tool](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) to discover connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="89d17-114">Use [test connectivity tool](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) to discover connectivity issues.</span></span>


## <a name="next-steps"></a><span data-ttu-id="89d17-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="89d17-115">Next steps</span></span>
* [<span data-ttu-id="89d17-116">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="89d17-116">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
