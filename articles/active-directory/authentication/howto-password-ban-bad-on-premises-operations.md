---
title: Azure AD password protection preview operations and reporting
description: Azure AD password protection preview post-deployment operations and reporting
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: jsimmons
ms.openlocfilehash: 14aa52b6d424423f4863efa63f3e2e66b84dac70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870426"
---
# <a name="preview-azure-ad-password-protection-post-deployment"></a><span data-ttu-id="a14f5-103">Preview: Azure AD password protection post-deployment</span><span class="sxs-lookup"><span data-stu-id="a14f5-103">Preview: Azure AD password protection post-deployment</span></span>

|     |
| --- |
| <span data-ttu-id="a14f5-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a14f5-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span></span> <span data-ttu-id="a14f5-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="a14f5-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>|
|     |

<span data-ttu-id="a14f5-106">After you have completed the [installation of Azure AD password protection](howto-password-ban-bad-on-premises.md) on-premises, there are a couple items that must be configured in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a14f5-106">After you have completed the [installation of Azure AD password protection](howto-password-ban-bad-on-premises.md) on-premises, there are a couple items that must be configured in the Azure portal.</span></span>

## <a name="configure-the-custom-banned-password-list"></a><span data-ttu-id="a14f5-107">Configure the custom banned password list</span><span class="sxs-lookup"><span data-stu-id="a14f5-107">Configure the custom banned password list</span></span>

<span data-ttu-id="a14f5-108">Follow the guidance in the article [Configuring the custom banned password list](howto-password-ban-bad.md) for steps to customize the banned password list for your organization.</span><span class="sxs-lookup"><span data-stu-id="a14f5-108">Follow the guidance in the article [Configuring the custom banned password list](howto-password-ban-bad.md) for steps to customize the banned password list for your organization.</span></span>

## <a name="enable-password-protection"></a><span data-ttu-id="a14f5-109">Enable password protection</span><span class="sxs-lookup"><span data-stu-id="a14f5-109">Enable password protection</span></span>

1. <span data-ttu-id="a14f5-110">Log in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory**, **Authentication methods**, then **Password protection (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="a14f5-110">Log in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory**, **Authentication methods**, then **Password protection (Preview)**.</span></span>
1. <span data-ttu-id="a14f5-111">Set **Enable password protection on Windows Server Active Directory** to **Yes**</span><span class="sxs-lookup"><span data-stu-id="a14f5-111">Set **Enable password protection on Windows Server Active Directory** to **Yes**</span></span>
1. <span data-ttu-id="a14f5-112">As mentioned in the [Deployment guide](howto-password-ban-bad-on-premises.md#deployment-strategy), it is recommended to initially set the **Mode** to **Audit**</span><span class="sxs-lookup"><span data-stu-id="a14f5-112">As mentioned in the [Deployment guide](howto-password-ban-bad-on-premises.md#deployment-strategy), it is recommended to initially set the **Mode** to **Audit**</span></span>
   * <span data-ttu-id="a14f5-113">After you are comfortable with the feature, you can switch the **Mode** to **Enforced**</span><span class="sxs-lookup"><span data-stu-id="a14f5-113">After you are comfortable with the feature, you can switch the **Mode** to **Enforced**</span></span>
1. <span data-ttu-id="a14f5-114">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="a14f5-114">Click **Save**</span></span>

![Enabling Azure AD password protection components in the Azure portal](./media/howto-password-ban-bad-on-premises-operations/authentication-methods-password-protection-on-prem.png)

## <a name="audit-mode"></a><span data-ttu-id="a14f5-116">Audit Mode</span><span class="sxs-lookup"><span data-stu-id="a14f5-116">Audit Mode</span></span>

<span data-ttu-id="a14f5-117">Audit mode is intended as a way to run the software in a “what if” mode.</span><span class="sxs-lookup"><span data-stu-id="a14f5-117">Audit mode is intended as a way to run the software in a “what if” mode.</span></span> <span data-ttu-id="a14f5-118">Each DC agent service evaluates an incoming password according to the currently active policy.</span><span class="sxs-lookup"><span data-stu-id="a14f5-118">Each DC agent service evaluates an incoming password according to the currently active policy.</span></span> <span data-ttu-id="a14f5-119">If the current policy is configured to be in Audit mode, “bad” passwords result in event log messages but are accepted.</span><span class="sxs-lookup"><span data-stu-id="a14f5-119">If the current policy is configured to be in Audit mode, “bad” passwords result in event log messages but are accepted.</span></span> <span data-ttu-id="a14f5-120">This is the only difference between Audit and Enforce mode; all other operations run the same.</span><span class="sxs-lookup"><span data-stu-id="a14f5-120">This is the only difference between Audit and Enforce mode; all other operations run the same.</span></span>

> [!NOTE]
> <span data-ttu-id="a14f5-121">Microsoft recommends that initial deployment and testing always start out in Audit mode.</span><span class="sxs-lookup"><span data-stu-id="a14f5-121">Microsoft recommends that initial deployment and testing always start out in Audit mode.</span></span> <span data-ttu-id="a14f5-122">Events in the event log should then be monitored to try to anticipate whether any existing operational processes would be disturbed once Enforce mode is enabled.</span><span class="sxs-lookup"><span data-stu-id="a14f5-122">Events in the event log should then be monitored to try to anticipate whether any existing operational processes would be disturbed once Enforce mode is enabled.</span></span>

## <a name="enforce-mode"></a><span data-ttu-id="a14f5-123">Enforce Mode</span><span class="sxs-lookup"><span data-stu-id="a14f5-123">Enforce Mode</span></span>

<span data-ttu-id="a14f5-124">Enforce mode is intended as the final configuration.</span><span class="sxs-lookup"><span data-stu-id="a14f5-124">Enforce mode is intended as the final configuration.</span></span> <span data-ttu-id="a14f5-125">As in Audit mode above, each DC agent service evaluates incoming passwords according to the currently active policy.</span><span class="sxs-lookup"><span data-stu-id="a14f5-125">As in Audit mode above, each DC agent service evaluates incoming passwords according to the currently active policy.</span></span> <span data-ttu-id="a14f5-126">If Enforce mode is enabled though, a password that is considered unsecure according to the policy is rejected.</span><span class="sxs-lookup"><span data-stu-id="a14f5-126">If Enforce mode is enabled though, a password that is considered unsecure according to the policy is rejected.</span></span>

<span data-ttu-id="a14f5-127">When a password is rejected in Enforce mode by the Azure AD password protection DC Agent, the visible impact seen by an end user is identical to what they would see if their password was rejected by traditional on-premises password complexity enforcement.</span><span class="sxs-lookup"><span data-stu-id="a14f5-127">When a password is rejected in Enforce mode by the Azure AD password protection DC Agent, the visible impact seen by an end user is identical to what they would see if their password was rejected by traditional on-premises password complexity enforcement.</span></span> <span data-ttu-id="a14f5-128">For example, a user might see the following traditional error message at the logon\change password screen:</span><span class="sxs-lookup"><span data-stu-id="a14f5-128">For example, a user might see the following traditional error message at the logon\change password screen:</span></span>

<span data-ttu-id="a14f5-129">“Unable to update the password.</span><span class="sxs-lookup"><span data-stu-id="a14f5-129">“Unable to update the password.</span></span> <span data-ttu-id="a14f5-130">The value provided for the new password does not meet the length, complexity, or history requirements of the domain.”</span><span class="sxs-lookup"><span data-stu-id="a14f5-130">The value provided for the new password does not meet the length, complexity, or history requirements of the domain.”</span></span>

<span data-ttu-id="a14f5-131">This message is only one example of several possible outcomes.</span><span class="sxs-lookup"><span data-stu-id="a14f5-131">This message is only one example of several possible outcomes.</span></span> <span data-ttu-id="a14f5-132">The specific error message can vary depending on the actual software or scenario that is attempting to set an unsecure password.</span><span class="sxs-lookup"><span data-stu-id="a14f5-132">The specific error message can vary depending on the actual software or scenario that is attempting to set an unsecure password.</span></span>

<span data-ttu-id="a14f5-133">Affected end users may need to work with their IT staff to understand the new requirements and be more able to choose secure passwords.</span><span class="sxs-lookup"><span data-stu-id="a14f5-133">Affected end users may need to work with their IT staff to understand the new requirements and be more able to choose secure passwords.</span></span>

## <a name="usage-reporting"></a><span data-ttu-id="a14f5-134">Usage reporting</span><span class="sxs-lookup"><span data-stu-id="a14f5-134">Usage reporting</span></span>

<span data-ttu-id="a14f5-135">The `Get-AzureADPasswordProtectionSummaryReport` cmdlet may be used to produce a summary view of activity.</span><span class="sxs-lookup"><span data-stu-id="a14f5-135">The `Get-AzureADPasswordProtectionSummaryReport` cmdlet may be used to produce a summary view of activity.</span></span> <span data-ttu-id="a14f5-136">An example output of this cmdlet is as follows:</span><span class="sxs-lookup"><span data-stu-id="a14f5-136">An example output of this cmdlet is as follows:</span></span>

```
Get-AzureADPasswordProtectionSummaryReport -DomainController bplrootdc2
DomainController                : bplrootdc2
PasswordChangesValidated        : 6677
PasswordSetsValidated           : 9
PasswordChangesRejected         : 10868
PasswordSetsRejected            : 34
PasswordChangeAuditOnlyFailures : 213
PasswordSetAuditOnlyFailures    : 3
PasswordChangeErrors            : 0
PasswordSetErrors               : 1
```

<span data-ttu-id="a14f5-137">The scope of the cmdlet’s reporting may be influenced using one of the –Forest, -Domain, or –DomainController parameters.</span><span class="sxs-lookup"><span data-stu-id="a14f5-137">The scope of the cmdlet’s reporting may be influenced using one of the –Forest, -Domain, or –DomainController parameters.</span></span> <span data-ttu-id="a14f5-138">Not specifying a parameter implies –Forest.</span><span class="sxs-lookup"><span data-stu-id="a14f5-138">Not specifying a parameter implies –Forest.</span></span>

> [!NOTE]
> <span data-ttu-id="a14f5-139">This cmdlet works by remotely querying each DC agent service’s Admin event log.</span><span class="sxs-lookup"><span data-stu-id="a14f5-139">This cmdlet works by remotely querying each DC agent service’s Admin event log.</span></span> <span data-ttu-id="a14f5-140">If the event logs contain large numbers of events, the cmdlet may take a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="a14f5-140">If the event logs contain large numbers of events, the cmdlet may take a long time to complete.</span></span> <span data-ttu-id="a14f5-141">In addition, bulk network queries of large data sets may impact domain controller performance.</span><span class="sxs-lookup"><span data-stu-id="a14f5-141">In addition, bulk network queries of large data sets may impact domain controller performance.</span></span> <span data-ttu-id="a14f5-142">Therefore, this cmdlet should be used carefully in production environments.</span><span class="sxs-lookup"><span data-stu-id="a14f5-142">Therefore, this cmdlet should be used carefully in production environments.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a14f5-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="a14f5-143">Next steps</span></span>

[<span data-ttu-id="a14f5-144">Troubleshooting and logging information for Azure AD password protection</span><span class="sxs-lookup"><span data-stu-id="a14f5-144">Troubleshooting and logging information for Azure AD password protection</span></span>](howto-password-ban-bad-on-premises-troubleshoot.md)
