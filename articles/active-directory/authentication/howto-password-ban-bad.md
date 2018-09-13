---
title: How to ban passwords in Azure AD
description: Ban weak passwords from your envirionment with Azure AD dynamically banned passwrords
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: rogoya
ms.openlocfilehash: 30d8260d78b3b46a9f4caea63f6bed818935a9a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866383"
---
# <a name="configuring-the-custom-banned-password-list"></a><span data-ttu-id="c20cc-103">Configuring the custom banned password list</span><span class="sxs-lookup"><span data-stu-id="c20cc-103">Configuring the custom banned password list</span></span>

|     |
| --- |
| <span data-ttu-id="c20cc-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c20cc-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span></span> <span data-ttu-id="c20cc-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="c20cc-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>|
|     |

<span data-ttu-id="c20cc-106">Many organizations find their users create passwords using common local words such as a school, sports team, or famous person, leaving them easy to guess.</span><span class="sxs-lookup"><span data-stu-id="c20cc-106">Many organizations find their users create passwords using common local words such as a school, sports team, or famous person, leaving them easy to guess.</span></span> <span data-ttu-id="c20cc-107">Microsoft's custom banned password list allows organizations to add strings to evaluate and block, in addition to the global banned password list, when users and administrators attempt to change or reset a password.</span><span class="sxs-lookup"><span data-stu-id="c20cc-107">Microsoft's custom banned password list allows organizations to add strings to evaluate and block, in addition to the global banned password list, when users and administrators attempt to change or reset a password.</span></span>

## <a name="add-to-the-custom-list"></a><span data-ttu-id="c20cc-108">Add to the custom list</span><span class="sxs-lookup"><span data-stu-id="c20cc-108">Add to the custom list</span></span>

<span data-ttu-id="c20cc-109">Configuring the custom banned password list requires an Azure Active Directory Premium P1 or P2 license.</span><span class="sxs-lookup"><span data-stu-id="c20cc-109">Configuring the custom banned password list requires an Azure Active Directory Premium P1 or P2 license.</span></span> <span data-ttu-id="c20cc-110">For more detailed information about Azure Active Directory licensing, see the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory/).|</span><span class="sxs-lookup"><span data-stu-id="c20cc-110">For more detailed information about Azure Active Directory licensing, see the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory/).|</span></span>

1. <span data-ttu-id="c20cc-111">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory**, **Authentication methods**, then **Password protection (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="c20cc-111">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory**, **Authentication methods**, then **Password protection (Preview)**.</span></span>
1. <span data-ttu-id="c20cc-112">Set the option **Enforce custom list**, to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c20cc-112">Set the option **Enforce custom list**, to **Yes**.</span></span>
1. <span data-ttu-id="c20cc-113">Add strings to the **Custom banned password list**, one string per line</span><span class="sxs-lookup"><span data-stu-id="c20cc-113">Add strings to the **Custom banned password list**, one string per line</span></span>
   * <span data-ttu-id="c20cc-114">The custom banned password list can contain up to 1000 words.</span><span class="sxs-lookup"><span data-stu-id="c20cc-114">The custom banned password list can contain up to 1000 words.</span></span>
   * <span data-ttu-id="c20cc-115">The custom banned password list is case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="c20cc-115">The custom banned password list is case-insensitive.</span></span>
   * <span data-ttu-id="c20cc-116">The custom banned password list considers common character substitution.</span><span class="sxs-lookup"><span data-stu-id="c20cc-116">The custom banned password list considers common character substitution.</span></span>
      * <span data-ttu-id="c20cc-117">Example: "o" and "0" or "a" and "@"</span><span class="sxs-lookup"><span data-stu-id="c20cc-117">Example: "o" and "0" or "a" and "@"</span></span>
   * <span data-ttu-id="c20cc-118">The minimum string length is four characters and the maximum is 16 characters.</span><span class="sxs-lookup"><span data-stu-id="c20cc-118">The minimum string length is four characters and the maximum is 16 characters.</span></span>
1. <span data-ttu-id="c20cc-119">When you have added all strings, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c20cc-119">When you have added all strings, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c20cc-120">It may take several hours for updates to the custom banned password list to be applied.</span><span class="sxs-lookup"><span data-stu-id="c20cc-120">It may take several hours for updates to the custom banned password list to be applied.</span></span>

![Modify the custom banned password list under Authentication Methods in the Azure portal](./media/howto-password-ban-bad/authentication-methods-password-protection.png)

## <a name="how-it-works"></a><span data-ttu-id="c20cc-122">How it works</span><span class="sxs-lookup"><span data-stu-id="c20cc-122">How it works</span></span>

<span data-ttu-id="c20cc-123">Each time a user or administrator resets or changes an Azure AD password, it flows through the banned password lists to confirm that it is not on a list.</span><span class="sxs-lookup"><span data-stu-id="c20cc-123">Each time a user or administrator resets or changes an Azure AD password, it flows through the banned password lists to confirm that it is not on a list.</span></span> <span data-ttu-id="c20cc-124">This check is included in any passwords set or changed using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c20cc-124">This check is included in any passwords set or changed using Azure AD.</span></span>

## <a name="what-do-users-see"></a><span data-ttu-id="c20cc-125">What do users see</span><span class="sxs-lookup"><span data-stu-id="c20cc-125">What do users see</span></span>

<span data-ttu-id="c20cc-126">When a user attempts to reset a password to something that would be banned, they see the following error message:</span><span class="sxs-lookup"><span data-stu-id="c20cc-126">When a user attempts to reset a password to something that would be banned, they see the following error message:</span></span>

<span data-ttu-id="c20cc-127">Unfortunately, your password contains a word, phrase, or pattern that makes your password easily guessable.</span><span class="sxs-lookup"><span data-stu-id="c20cc-127">Unfortunately, your password contains a word, phrase, or pattern that makes your password easily guessable.</span></span> <span data-ttu-id="c20cc-128">Please try again with a different password.</span><span class="sxs-lookup"><span data-stu-id="c20cc-128">Please try again with a different password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c20cc-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="c20cc-129">Next steps</span></span>

[<span data-ttu-id="c20cc-130">Conceptual overview of the banned password lists</span><span class="sxs-lookup"><span data-stu-id="c20cc-130">Conceptual overview of the banned password lists</span></span>](concept-password-ban-bad.md)

[<span data-ttu-id="c20cc-131">Conceptual overview of Azure AD password protection</span><span class="sxs-lookup"><span data-stu-id="c20cc-131">Conceptual overview of Azure AD password protection</span></span>](concept-password-ban-bad-on-premises.md)

[<span data-ttu-id="c20cc-132">Enable on-premises integration with the banned password lists</span><span class="sxs-lookup"><span data-stu-id="c20cc-132">Enable on-premises integration with the banned password lists</span></span>](howto-password-ban-bad-on-premises.md)
