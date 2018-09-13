---
title: B2B collaboration for hybrid organizations - Azure Active Directory | Microsoft Docs
description: Give partners access to both on-premises and cloud resources with Azure AD B2B collaboration.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 04/26/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: eeeff6b41946f7f30fe728b5d2b863a25f466de8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856986"
---
# <a name="azure-active-directory-b2b-collaboration-for-hybrid-organizations"></a><span data-ttu-id="53c3b-103">Azure Active Directory B2B collaboration for hybrid organizations</span><span class="sxs-lookup"><span data-stu-id="53c3b-103">Azure Active Directory B2B collaboration for hybrid organizations</span></span>

<span data-ttu-id="53c3b-104">Azure Active Directory (Azure AD) B2B collaboration makes it easy for you to give your external partners access to apps and resources in your organization.</span><span class="sxs-lookup"><span data-stu-id="53c3b-104">Azure Active Directory (Azure AD) B2B collaboration makes it easy for you to give your external partners access to apps and resources in your organization.</span></span> <span data-ttu-id="53c3b-105">This is true even in a hybrid configuration where you have both on-premises and cloud-based resources.</span><span class="sxs-lookup"><span data-stu-id="53c3b-105">This is true even in a hybrid configuration where you have both on-premises and cloud-based resources.</span></span> <span data-ttu-id="53c3b-106">It doesn’t matter if you currently manage external partner accounts locally in your on-premises identity system, or if you manage the external accounts in the cloud as Azure AD B2B users.</span><span class="sxs-lookup"><span data-stu-id="53c3b-106">It doesn’t matter if you currently manage external partner accounts locally in your on-premises identity system, or if you manage the external accounts in the cloud as Azure AD B2B users.</span></span> <span data-ttu-id="53c3b-107">You can now grant these users access to resources in either location, using the same sign-in credentials for both environments.</span><span class="sxs-lookup"><span data-stu-id="53c3b-107">You can now grant these users access to resources in either location, using the same sign-in credentials for both environments.</span></span>

## <a name="grant-b2b-users-in-azure-ad-access-to-your-on-premises-apps"></a><span data-ttu-id="53c3b-108">Grant B2B users in Azure AD access to your on-premises apps</span><span class="sxs-lookup"><span data-stu-id="53c3b-108">Grant B2B users in Azure AD access to your on-premises apps</span></span>

<span data-ttu-id="53c3b-109">If your organization uses Azure AD B2B collaboration capabilities to invite guest users from partner organizations to your Azure AD, you can now provide these B2B users access to on-premises apps.</span><span class="sxs-lookup"><span data-stu-id="53c3b-109">If your organization uses Azure AD B2B collaboration capabilities to invite guest users from partner organizations to your Azure AD, you can now provide these B2B users access to on-premises apps.</span></span>

<span data-ttu-id="53c3b-110">For apps that use SAML-based authentication, you can make these apps available to B2B users through the Azure portal, using Azure AD Application Proxy for authentication.</span><span class="sxs-lookup"><span data-stu-id="53c3b-110">For apps that use SAML-based authentication, you can make these apps available to B2B users through the Azure portal, using Azure AD Application Proxy for authentication.</span></span>

<span data-ttu-id="53c3b-111">For apps that use Integrated Windows Authentication (IWA) with Kerberos constrained delegation (KCD), you also use Azure AD Proxy for authentication.</span><span class="sxs-lookup"><span data-stu-id="53c3b-111">For apps that use Integrated Windows Authentication (IWA) with Kerberos constrained delegation (KCD), you also use Azure AD Proxy for authentication.</span></span> <span data-ttu-id="53c3b-112">However, for authorization to work, a user object is required in the on-premises Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="53c3b-112">However, for authorization to work, a user object is required in the on-premises Windows Server Active Directory.</span></span> <span data-ttu-id="53c3b-113">There are two methods you can use to create local user objects that represent your B2B guest users.</span><span class="sxs-lookup"><span data-stu-id="53c3b-113">There are two methods you can use to create local user objects that represent your B2B guest users.</span></span>

- <span data-ttu-id="53c3b-114">You can use Microsoft Identity Manager (MIM) 2016 SP1 and the MIM management agent for Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="53c3b-114">You can use Microsoft Identity Manager (MIM) 2016 SP1 and the MIM management agent for Microsoft Graph.</span></span>
- <span data-ttu-id="53c3b-115">You can use a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="53c3b-115">You can use a PowerShell script.</span></span> <span data-ttu-id="53c3b-116">(This solution does not require MIM.)</span><span class="sxs-lookup"><span data-stu-id="53c3b-116">(This solution does not require MIM.)</span></span>

<span data-ttu-id="53c3b-117">For details about how to implement these solutions, see [Grant B2B users in Azure AD access to your on-premises applications](hybrid-cloud-to-on-premises.md).</span><span class="sxs-lookup"><span data-stu-id="53c3b-117">For details about how to implement these solutions, see [Grant B2B users in Azure AD access to your on-premises applications](hybrid-cloud-to-on-premises.md).</span></span>

## <a name="grant-locally-managed-partner-accounts-access-to-cloud-resources"></a><span data-ttu-id="53c3b-118">Grant locally-managed partner accounts access to cloud resources</span><span class="sxs-lookup"><span data-stu-id="53c3b-118">Grant locally-managed partner accounts access to cloud resources</span></span>

<span data-ttu-id="53c3b-119">Before Azure AD, organizations with on-premises identity systems have traditionally managed partner accounts in their on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="53c3b-119">Before Azure AD, organizations with on-premises identity systems have traditionally managed partner accounts in their on-premises directory.</span></span> <span data-ttu-id="53c3b-120">If you’re such an organization, you want to make sure that your partners continue to have access as you move your apps and other resources to the cloud.</span><span class="sxs-lookup"><span data-stu-id="53c3b-120">If you’re such an organization, you want to make sure that your partners continue to have access as you move your apps and other resources to the cloud.</span></span> <span data-ttu-id="53c3b-121">Ideally, you want these users to use the same set of credentials to access both cloud and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="53c3b-121">Ideally, you want these users to use the same set of credentials to access both cloud and on-premises resources.</span></span> 

<span data-ttu-id="53c3b-122">We now offer methods where you can use Azure AD Connect to sync these local accounts to the cloud as "guest users," where the accounts behave just like Azure AD B2B users.</span><span class="sxs-lookup"><span data-stu-id="53c3b-122">We now offer methods where you can use Azure AD Connect to sync these local accounts to the cloud as "guest users," where the accounts behave just like Azure AD B2B users.</span></span>

<span data-ttu-id="53c3b-123">To help protect your company data, you can control access to just the right resources, and configure authorization policies that treat these guest users differently from your employees.</span><span class="sxs-lookup"><span data-stu-id="53c3b-123">To help protect your company data, you can control access to just the right resources, and configure authorization policies that treat these guest users differently from your employees.</span></span>

<span data-ttu-id="53c3b-124">For implementation details, see [Grant locally-managed partner accounts access to cloud resources using Azure AD B2B collaboration](hybrid-on-premises-to-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="53c3b-124">For implementation details, see [Grant locally-managed partner accounts access to cloud resources using Azure AD B2B collaboration](hybrid-on-premises-to-cloud.md).</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="53c3b-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="53c3b-125">Next steps</span></span>

- [<span data-ttu-id="53c3b-126">Grant B2B users in Azure AD access to your on-premises applications</span><span class="sxs-lookup"><span data-stu-id="53c3b-126">Grant B2B users in Azure AD access to your on-premises applications</span></span>](hybrid-cloud-to-on-premises.md)
- [<span data-ttu-id="53c3b-127">Grant locally-managed partner accounts access to cloud resources using Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="53c3b-127">Grant locally-managed partner accounts access to cloud resources using Azure AD B2B collaboration</span></span>](hybrid-on-premises-to-cloud.md)


