---
title: What is Azure Active Directory B2B collaboration? | Microsoft Docs
description: Azure Active Directory B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 04/26/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 51a969ae215583a0be8d75ff1de11173e0696a22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968799"
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="23efe-104">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="23efe-104">What is Azure AD B2B collaboration?</span></span>

<span data-ttu-id="23efe-105">Azure Active Directory (Azure AD) business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span><span class="sxs-lookup"><span data-stu-id="23efe-105">Azure Active Directory (Azure AD) business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="23efe-106">Those organizations can be with or without Azure AD, and don't even need to have an IT department.</span><span class="sxs-lookup"><span data-stu-id="23efe-106">Those organizations can be with or without Azure AD, and don't even need to have an IT department.</span></span>

<span data-ttu-id="23efe-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span><span class="sxs-lookup"><span data-stu-id="23efe-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="23efe-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span><span class="sxs-lookup"><span data-stu-id="23efe-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="23efe-109">Also, it's easy for end users to navigate.</span><span class="sxs-lookup"><span data-stu-id="23efe-109">Also, it's easy for end users to navigate.</span></span>

<span data-ttu-id="23efe-110">The following video provides a useful overview.</span><span class="sxs-lookup"><span data-stu-id="23efe-110">The following video provides a useful overview.</span></span>
>[!VIDEO https://www.youtube.com/embed/AhwrweCBdsc]

## <a name="key-benefits-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="23efe-111">Key benefits of Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="23efe-111">Key benefits of Azure AD B2B collaboration</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="23efe-112">Work with any user from any partner</span><span class="sxs-lookup"><span data-stu-id="23efe-112">Work with any user from any partner</span></span>

- <span data-ttu-id="23efe-113">Partners use their own credentials</span><span class="sxs-lookup"><span data-stu-id="23efe-113">Partners use their own credentials</span></span>
- <span data-ttu-id="23efe-114">No requirement for partners to use Azure AD</span><span class="sxs-lookup"><span data-stu-id="23efe-114">No requirement for partners to use Azure AD</span></span>
- <span data-ttu-id="23efe-115">No external directories or complex set-up required</span><span class="sxs-lookup"><span data-stu-id="23efe-115">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="23efe-116">Simple and secure collaboration</span><span class="sxs-lookup"><span data-stu-id="23efe-116">Simple and secure collaboration</span></span>

- <span data-ttu-id="23efe-117">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span><span class="sxs-lookup"><span data-stu-id="23efe-117">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>
- <span data-ttu-id="23efe-118">Easy for users</span><span class="sxs-lookup"><span data-stu-id="23efe-118">Easy for users</span></span>
- <span data-ttu-id="23efe-119">Enterprise-grade security for apps and data</span><span class="sxs-lookup"><span data-stu-id="23efe-119">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="23efe-120">No management overhead</span><span class="sxs-lookup"><span data-stu-id="23efe-120">No management overhead</span></span>

- <span data-ttu-id="23efe-121">No external account or password management</span><span class="sxs-lookup"><span data-stu-id="23efe-121">No external account or password management</span></span>
- <span data-ttu-id="23efe-122">No sync or manual account lifecycle management</span><span class="sxs-lookup"><span data-stu-id="23efe-122">No sync or manual account lifecycle management</span></span>
- <span data-ttu-id="23efe-123">No external administrative overhead</span><span class="sxs-lookup"><span data-stu-id="23efe-123">No external administrative overhead</span></span>

## <a name="easily-add-b2b-collaboration-users"></a><span data-ttu-id="23efe-124">Easily add B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="23efe-124">Easily add B2B collaboration users</span></span>

<span data-ttu-id="23efe-125">As an administrator, you can easily add B2B collaboration (guest) users to your organization in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23efe-125">As an administrator, you can easily add B2B collaboration (guest) users to your organization in the [Azure portal](https://portal.azure.com).</span></span>

![add guest users](media/what-is-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="23efe-127">Enable your collaborators to bring their own identity</span><span class="sxs-lookup"><span data-stu-id="23efe-127">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="23efe-128">B2B collaborators can sign in with an identity of their choice.</span><span class="sxs-lookup"><span data-stu-id="23efe-128">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="23efe-129">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span><span class="sxs-lookup"><span data-stu-id="23efe-129">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="23efe-130">Delegate to application and group owners</span><span class="sxs-lookup"><span data-stu-id="23efe-130">Delegate to application and group owners</span></span>

<span data-ttu-id="23efe-131">As an application or group owner, you can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span><span class="sxs-lookup"><span data-stu-id="23efe-131">As an application or group owner, you can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="23efe-132">Administrators can delegate permission to add B2B users to non-administrators.</span><span class="sxs-lookup"><span data-stu-id="23efe-132">Administrators can delegate permission to add B2B users to non-administrators.</span></span> <span data-ttu-id="23efe-133">Non-administrators can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span><span class="sxs-lookup"><span data-stu-id="23efe-133">Non-administrators can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![access panel](media/what-is-b2b/access-panel.png)

![add member](media/what-is-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="23efe-136">Authorization policies protect your corporate content</span><span class="sxs-lookup"><span data-stu-id="23efe-136">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="23efe-137">Conditional access policies, such as multi-factor authentication, can be enforced:</span><span class="sxs-lookup"><span data-stu-id="23efe-137">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="23efe-138">At the tenant level</span><span class="sxs-lookup"><span data-stu-id="23efe-138">At the tenant level</span></span>
- <span data-ttu-id="23efe-139">At the application level</span><span class="sxs-lookup"><span data-stu-id="23efe-139">At the application level</span></span>
- <span data-ttu-id="23efe-140">For specific users to protect corporate apps and data</span><span class="sxs-lookup"><span data-stu-id="23efe-140">For specific users to protect corporate apps and data</span></span>

### <a name="use-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="23efe-141">Use APIs and sample code to easily build applications to onboard</span><span class="sxs-lookup"><span data-stu-id="23efe-141">Use APIs and sample code to easily build applications to onboard</span></span>

<span data-ttu-id="23efe-142">Bring your external partners on board in ways customized to your organization’s needs.</span><span class="sxs-lookup"><span data-stu-id="23efe-142">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="23efe-143">Use the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) to customize your onboarding experiences, including creating self-service sign-up portals.</span><span class="sxs-lookup"><span data-stu-id="23efe-143">Use the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) to customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="23efe-144">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="23efe-144">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![sign-up portal](media/what-is-b2b/sign-up-portal.png)

<span data-ttu-id="23efe-146">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span><span class="sxs-lookup"><span data-stu-id="23efe-146">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23efe-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="23efe-147">Next steps</span></span>

- [<span data-ttu-id="23efe-148">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="23efe-148">How do Azure Active Directory admins add B2B collaboration users?</span></span>](add-users-administrator.md)
- [<span data-ttu-id="23efe-149">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="23efe-149">How do information workers add B2B collaboration users?</span></span>](add-users-information-worker.md)
- [<span data-ttu-id="23efe-150">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="23efe-150">B2B collaboration invitation redemption</span></span>](redemption-experience.md)
- [<span data-ttu-id="23efe-151">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="23efe-151">Azure AD B2B collaboration licensing</span></span>](licensing-guidance.md)
- <span data-ttu-id="23efe-152">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="23efe-152">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>