---
title: Dynamically banned passwords in Azure AD
description: Ban weak passwords from your environment with Azure AD dynamically banned passwords
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: rogoya
ms.openlocfilehash: 1ad499e2703ff8376c063d933c0cc1f03765fc23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869024"
---
# <a name="eliminate-bad-passwords-in-your-organization"></a><span data-ttu-id="3c47d-103">Eliminate bad passwords in your organization</span><span class="sxs-lookup"><span data-stu-id="3c47d-103">Eliminate bad passwords in your organization</span></span>

|     |
| --- |
| <span data-ttu-id="3c47d-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c47d-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span></span> <span data-ttu-id="3c47d-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="3c47d-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>|
|     |

<span data-ttu-id="3c47d-106">Industry leaders tell you not to use the same password in multiple places, to make it complex, and to not make it simple like Password123.</span><span class="sxs-lookup"><span data-stu-id="3c47d-106">Industry leaders tell you not to use the same password in multiple places, to make it complex, and to not make it simple like Password123.</span></span> <span data-ttu-id="3c47d-107">How can organizations guarantee that their users are following guidance?</span><span class="sxs-lookup"><span data-stu-id="3c47d-107">How can organizations guarantee that their users are following guidance?</span></span> <span data-ttu-id="3c47d-108">How can they make sure users aren't using common passwords or passwords that are known to be included in recent data breaches?</span><span class="sxs-lookup"><span data-stu-id="3c47d-108">How can they make sure users aren't using common passwords or passwords that are known to be included in recent data breaches?</span></span>

## <a name="global-banned-password-list"></a><span data-ttu-id="3c47d-109">Global banned password list</span><span class="sxs-lookup"><span data-stu-id="3c47d-109">Global banned password list</span></span>

<span data-ttu-id="3c47d-110">Microsoft is always working to stay one step ahead of cyber-criminals.</span><span class="sxs-lookup"><span data-stu-id="3c47d-110">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span> <span data-ttu-id="3c47d-111">Therefore the Azure AD Identity Protection team continually look for commonly used and compromised passwords.</span><span class="sxs-lookup"><span data-stu-id="3c47d-111">Therefore the Azure AD Identity Protection team continually look for commonly used and compromised passwords.</span></span> <span data-ttu-id="3c47d-112">They then block those passwords that are deemed too common in what is called the global banned password list.</span><span class="sxs-lookup"><span data-stu-id="3c47d-112">They then block those passwords that are deemed too common in what is called the global banned password list.</span></span> <span data-ttu-id="3c47d-113">Cyber-criminals also use similar strategies in their attacks, therefore Microsoft does not publish the contents of this list publicly.</span><span class="sxs-lookup"><span data-stu-id="3c47d-113">Cyber-criminals also use similar strategies in their attacks, therefore Microsoft does not publish the contents of this list publicly.</span></span> <span data-ttu-id="3c47d-114">These vulnerable passwords are blocked before they become a real threat to Microsoft's customers.</span><span class="sxs-lookup"><span data-stu-id="3c47d-114">These vulnerable passwords are blocked before they become a real threat to Microsoft's customers.</span></span> <span data-ttu-id="3c47d-115">For more information about current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/intelligence-report).</span><span class="sxs-lookup"><span data-stu-id="3c47d-115">For more information about current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/intelligence-report).</span></span>

## <a name="preview-custom-banned-password-list"></a><span data-ttu-id="3c47d-116">Preview: Custom banned password list</span><span class="sxs-lookup"><span data-stu-id="3c47d-116">Preview: Custom banned password list</span></span>

<span data-ttu-id="3c47d-117">Some organizations may want to take security one step further by adding their own customizations on top of the global banned password list in what Microsoft calls the custom banned password list.</span><span class="sxs-lookup"><span data-stu-id="3c47d-117">Some organizations may want to take security one step further by adding their own customizations on top of the global banned password list in what Microsoft calls the custom banned password list.</span></span> <span data-ttu-id="3c47d-118">Enterprise customers like Contoso could then choose to block variants of their brand names, company-specific terms, or other items.</span><span class="sxs-lookup"><span data-stu-id="3c47d-118">Enterprise customers like Contoso could then choose to block variants of their brand names, company-specific terms, or other items.</span></span>

<span data-ttu-id="3c47d-119">The custom banned password list and the ability to enable on-premises Active Directory integration is managed using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3c47d-119">The custom banned password list and the ability to enable on-premises Active Directory integration is managed using the Azure portal.</span></span>

![Modify the custom banned password list under Authentication Methods in the Azure portal](./media/concept-password-ban-bad/authentication-methods-password-protection.png)

## <a name="on-premises-hybrid-scenarios"></a><span data-ttu-id="3c47d-121">On-premises hybrid scenarios</span><span class="sxs-lookup"><span data-stu-id="3c47d-121">On-premises hybrid scenarios</span></span>

<span data-ttu-id="3c47d-122">Protecting cloud-only accounts is helpful but many organizations maintain hybrid scenarios including on-premises Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c47d-122">Protecting cloud-only accounts is helpful but many organizations maintain hybrid scenarios including on-premises Windows Server Active Directory.</span></span> <span data-ttu-id="3c47d-123">It is possible to install Azure AD password protection for Windows Server Active Directory (preview) agents on-premises to extend the banned password lists to your existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="3c47d-123">It is possible to install Azure AD password protection for Windows Server Active Directory (preview) agents on-premises to extend the banned password lists to your existing infrastructure.</span></span> <span data-ttu-id="3c47d-124">Now users and administrators who change, set, or reset passwords on-premises are required to comply with the same password policy as cloud-only users.</span><span class="sxs-lookup"><span data-stu-id="3c47d-124">Now users and administrators who change, set, or reset passwords on-premises are required to comply with the same password policy as cloud-only users.</span></span>

## <a name="how-does-the-banned-password-list-work"></a><span data-ttu-id="3c47d-125">How does the banned password list work</span><span class="sxs-lookup"><span data-stu-id="3c47d-125">How does the banned password list work</span></span>

<span data-ttu-id="3c47d-126">The banned password list matches passwords in the list by converting the string to lowercase and comparing to the known banned passwords within an edit distance of 1 with fuzzy matching.</span><span class="sxs-lookup"><span data-stu-id="3c47d-126">The banned password list matches passwords in the list by converting the string to lowercase and comparing to the known banned passwords within an edit distance of 1 with fuzzy matching.</span></span>

<span data-ttu-id="3c47d-127">Example: The word password is blocked for an organization</span><span class="sxs-lookup"><span data-stu-id="3c47d-127">Example: The word password is blocked for an organization</span></span>
   - <span data-ttu-id="3c47d-128">A user tries to set their password to "P@ssword" that is converted to "password" and because it is a variant of password is blocked.</span><span class="sxs-lookup"><span data-stu-id="3c47d-128">A user tries to set their password to "P@ssword" that is converted to "password" and because it is a variant of password is blocked.</span></span>
   - <span data-ttu-id="3c47d-129">An administrator attempts to set a users password to "Password123!"</span><span class="sxs-lookup"><span data-stu-id="3c47d-129">An administrator attempts to set a users password to "Password123!"</span></span> <span data-ttu-id="3c47d-130">that converted to "password123!"</span><span class="sxs-lookup"><span data-stu-id="3c47d-130">that converted to "password123!"</span></span> <span data-ttu-id="3c47d-131">and because it is a variant of password is blocked.</span><span class="sxs-lookup"><span data-stu-id="3c47d-131">and because it is a variant of password is blocked.</span></span>

<span data-ttu-id="3c47d-132">Each time a user resets or changes their Azure AD password it flows through this process to confirm that it is not on the banned password list.</span><span class="sxs-lookup"><span data-stu-id="3c47d-132">Each time a user resets or changes their Azure AD password it flows through this process to confirm that it is not on the banned password list.</span></span> <span data-ttu-id="3c47d-133">This check is included in hybrid scenarios using self-service password reset, password hash sync, and pass-through authentication.</span><span class="sxs-lookup"><span data-stu-id="3c47d-133">This check is included in hybrid scenarios using self-service password reset, password hash sync, and pass-through authentication.</span></span>

## <a name="license-requirements"></a><span data-ttu-id="3c47d-134">License requirements</span><span class="sxs-lookup"><span data-stu-id="3c47d-134">License requirements</span></span>

|   | <span data-ttu-id="3c47d-135">Azure AD password protection with global banned password list</span><span class="sxs-lookup"><span data-stu-id="3c47d-135">Azure AD password protection with global banned password list</span></span> | <span data-ttu-id="3c47d-136">Azure AD password protection with custom banned password list</span><span class="sxs-lookup"><span data-stu-id="3c47d-136">Azure AD password protection with custom banned password list</span></span>|
| --- | --- | --- |
| <span data-ttu-id="3c47d-137">Cloud-only users</span><span class="sxs-lookup"><span data-stu-id="3c47d-137">Cloud-only users</span></span> | <span data-ttu-id="3c47d-138">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="3c47d-138">Azure AD Free</span></span> | <span data-ttu-id="3c47d-139">Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="3c47d-139">Azure AD Basic</span></span> |
| <span data-ttu-id="3c47d-140">Users synchronized from on-premises Windows Server Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c47d-140">Users synchronized from on-premises Windows Server Active Directory</span></span> | <span data-ttu-id="3c47d-141">Azure AD Premium P1 or P2</span><span class="sxs-lookup"><span data-stu-id="3c47d-141">Azure AD Premium P1 or P2</span></span> | <span data-ttu-id="3c47d-142">Azure AD Premium P1 or P2</span><span class="sxs-lookup"><span data-stu-id="3c47d-142">Azure AD Premium P1 or P2</span></span> |

<span data-ttu-id="3c47d-143">Additional licensing information, including costs, can be found on the [Azure Active Directory pricing site](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="3c47d-143">Additional licensing information, including costs, can be found on the [Azure Active Directory pricing site](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="what-do-users-see"></a><span data-ttu-id="3c47d-144">What do users see</span><span class="sxs-lookup"><span data-stu-id="3c47d-144">What do users see</span></span>

<span data-ttu-id="3c47d-145">When a user attempts to reset a password to something that would be banned, they see the following error message:</span><span class="sxs-lookup"><span data-stu-id="3c47d-145">When a user attempts to reset a password to something that would be banned, they see the following error message:</span></span>

<span data-ttu-id="3c47d-146">Unfortunately, your password contains a word, phrase, or pattern that makes your password easily guessable.</span><span class="sxs-lookup"><span data-stu-id="3c47d-146">Unfortunately, your password contains a word, phrase, or pattern that makes your password easily guessable.</span></span> <span data-ttu-id="3c47d-147">Please try again with a different password.</span><span class="sxs-lookup"><span data-stu-id="3c47d-147">Please try again with a different password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c47d-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c47d-148">Next steps</span></span>

* [<span data-ttu-id="3c47d-149">Configure the custom banned password list</span><span class="sxs-lookup"><span data-stu-id="3c47d-149">Configure the custom banned password list</span></span>](howto-password-ban-bad.md)
* [<span data-ttu-id="3c47d-150">Enable Azure AD password protection agents on-premises</span><span class="sxs-lookup"><span data-stu-id="3c47d-150">Enable Azure AD password protection agents on-premises</span></span>](howto-password-ban-bad-on-premises.md)
