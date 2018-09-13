---
title: Secure passwords  in Azure AD and reset passwords that get blocked by Smart Password Lockout | Microsoft Docs
description: Explains what an Azure AD tenant is, and how to manage Azure through Azure Active Directory
services: active-directory
documentationcenter: ''
author: markvi
writer: v-lorisc
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/02/2017
ms.author: markvi
ms.openlocfilehash: 4dd617a5493df4fe9c04167ea31391e69b0fb4fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671524"
---
# <a name="secure-passwords--in-azure-ad-and-reset-passwords-that-get-blocked-by-smart-password-lockout"></a><span data-ttu-id="9a979-103">Secure passwords  in Azure AD and reset passwords that get blocked by Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="9a979-103">Secure passwords  in Azure AD and reset passwords that get blocked by Smart Password Lockout</span></span>
<span data-ttu-id="9a979-104">This article discusses best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) and Microsoft Account Service accounts.</span><span class="sxs-lookup"><span data-stu-id="9a979-104">This article discusses best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) and Microsoft Account Service accounts.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="9a979-105">Azure AD administrators can reset user passwords by clicking the directory name.</span><span class="sxs-lookup"><span data-stu-id="9a979-105">Azure AD administrators can reset user passwords by clicking the directory name.</span></span> <span data-ttu-id="9a979-106">From the [Azure Management portal](https://manage.windowsazure.com), choose the Users page, click the name of the user, and Reset Password.</span><span class="sxs-lookup"><span data-stu-id="9a979-106">From the [Azure Management portal](https://manage.windowsazure.com), choose the Users page, click the name of the user, and Reset Password.</span></span> 
 >

<span data-ttu-id="9a979-107">Azure AD incorporates the following common approaches to securing passwords:</span><span class="sxs-lookup"><span data-stu-id="9a979-107">Azure AD incorporates the following common approaches to securing passwords:</span></span>
 *  <span data-ttu-id="9a979-108">Password length requirements</span><span class="sxs-lookup"><span data-stu-id="9a979-108">Password length requirements</span></span>
 *  <span data-ttu-id="9a979-109">Password “complexity” requirements</span><span class="sxs-lookup"><span data-stu-id="9a979-109">Password “complexity” requirements</span></span>
 *  <span data-ttu-id="9a979-110">Regular and periodic password expiration</span><span class="sxs-lookup"><span data-stu-id="9a979-110">Regular and periodic password expiration</span></span> 

<span data-ttu-id="9a979-111">For information about password management capabilities, see [Manage passwords in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-manage-passwords).</span><span class="sxs-lookup"><span data-stu-id="9a979-111">For information about password management capabilities, see [Manage passwords in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-manage-passwords).</span></span> 

## <a name="azure-ad-password-protection"></a><span data-ttu-id="9a979-112">Azure AD password protection</span><span class="sxs-lookup"><span data-stu-id="9a979-112">Azure AD password protection</span></span>
<span data-ttu-id="9a979-113">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords.</span><span class="sxs-lookup"><span data-stu-id="9a979-113">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords.</span></span> 

<span data-ttu-id="9a979-114">This section discusses how Azure AD protects passwords using the following methods:</span><span class="sxs-lookup"><span data-stu-id="9a979-114">This section discusses how Azure AD protects passwords using the following methods:</span></span>
 *  <span data-ttu-id="9a979-115">Dynamically banned passwords</span><span class="sxs-lookup"><span data-stu-id="9a979-115">Dynamically banned passwords</span></span>
 *  <span data-ttu-id="9a979-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="9a979-116">Smart Password Lockout</span></span>

<span data-ttu-id="9a979-117">For information about password management based on current research, see the [Password Guidance](http://aka.ms/passwordguidance) whitepaper.</span><span class="sxs-lookup"><span data-stu-id="9a979-117">For information about password management based on current research, see the [Password Guidance](http://aka.ms/passwordguidance) whitepaper.</span></span> 

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="9a979-118">Dynamically banned passwords</span><span class="sxs-lookup"><span data-stu-id="9a979-118">Dynamically banned passwords</span></span>
<span data-ttu-id="9a979-119">Azure AD and Microsoft Account System safeguard password protection by dynamically banning all commonly used passwords.</span><span class="sxs-lookup"><span data-stu-id="9a979-119">Azure AD and Microsoft Account System safeguard password protection by dynamically banning all commonly used passwords.</span></span> <span data-ttu-id="9a979-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span><span class="sxs-lookup"><span data-stu-id="9a979-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="9a979-121">This service is available to Azure AD and the Microsoft Account Service customers.</span><span class="sxs-lookup"><span data-stu-id="9a979-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span> 

<span data-ttu-id="9a979-122">When creating passwords, it is important for administrators to encourage users to choose uncommon password phrases that include a unique combination of letters, numbers, and characters.</span><span class="sxs-lookup"><span data-stu-id="9a979-122">When creating passwords, it is important for administrators to encourage users to choose uncommon password phrases that include a unique combination of letters, numbers, and characters.</span></span> <span data-ttu-id="9a979-123">This helps to make user passwords nearly impossible to be compromised.</span><span class="sxs-lookup"><span data-stu-id="9a979-123">This helps to make user passwords nearly impossible to be compromised.</span></span> 

<span data-ttu-id="9a979-124">**Breach lists**</span><span class="sxs-lookup"><span data-stu-id="9a979-124">**Breach lists**</span></span>

<span data-ttu-id="9a979-125">Azure AD is always working to stay one step ahead of cyber-criminals.</span><span class="sxs-lookup"><span data-stu-id="9a979-125">Azure AD is always working to stay one step ahead of cyber-criminals.</span></span> <span data-ttu-id="9a979-126">One way we do that is by preventing users from creating passwords that are on the current attack list.</span><span class="sxs-lookup"><span data-stu-id="9a979-126">One way we do that is by preventing users from creating passwords that are on the current attack list.</span></span>

<span data-ttu-id="9a979-127">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span><span class="sxs-lookup"><span data-stu-id="9a979-127">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="9a979-128">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span><span class="sxs-lookup"><span data-stu-id="9a979-128">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span> 

<span data-ttu-id="9a979-129">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span><span class="sxs-lookup"><span data-stu-id="9a979-129">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="9a979-130">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a979-130">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span> 

### <a name="smart-password-lockout"></a><span data-ttu-id="9a979-131">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="9a979-131">Smart Password Lockout</span></span>

<span data-ttu-id="9a979-132">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span><span class="sxs-lookup"><span data-stu-id="9a979-132">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="9a979-133">Azure AD is designed to determine the risk associated with specific login sessions.</span><span class="sxs-lookup"><span data-stu-id="9a979-133">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> 

<span data-ttu-id="9a979-134">Using the most up-to-date security data, we apply lockout semantics to cyber threats.</span><span class="sxs-lookup"><span data-stu-id="9a979-134">Using the most up-to-date security data, we apply lockout semantics to cyber threats.</span></span> <span data-ttu-id="9a979-135">This way users won’t get locked out, in the case when a cyber-criminal has hacked into user passwords on your network.</span><span class="sxs-lookup"><span data-stu-id="9a979-135">This way users won’t get locked out, in the case when a cyber-criminal has hacked into user passwords on your network.</span></span>

<span data-ttu-id="9a979-136">If a user is locked out of Azure AD, their screen looks similar to the one below:</span><span class="sxs-lookup"><span data-stu-id="9a979-136">If a user is locked out of Azure AD, their screen looks similar to the one below:</span></span>

  ![Locked out of Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-secure-passwords/locked-out-azuread.png)
  
<span data-ttu-id="9a979-138">And for other Microsoft accounts, their screen looks similar to the one below:</span><span class="sxs-lookup"><span data-stu-id="9a979-138">And for other Microsoft accounts, their screen looks similar to the one below:</span></span>

  ![Locked out of a Microsoft account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="9a979-140">For information about password management in Azure Active Directory, see [How password management works](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-how-it-works).</span><span class="sxs-lookup"><span data-stu-id="9a979-140">For information about password management in Azure Active Directory, see [How password management works](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-how-it-works).</span></span>

  ><span data-ttu-id="9a979-141">![NOTE] If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/en-us/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span><span class="sxs-lookup"><span data-stu-id="9a979-141">![NOTE] If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/en-us/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="9a979-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a979-142">Next steps</span></span>
[<span data-ttu-id="9a979-143">How to update your own password</span><span class="sxs-lookup"><span data-stu-id="9a979-143">How to update your own password</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-update-your-own-password)<br>
[<span data-ttu-id="9a979-144">The fundamentals of Azure identity management</span><span class="sxs-lookup"><span data-stu-id="9a979-144">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>
[<span data-ttu-id="9a979-145">How to get operational insights with password management reports</span><span class="sxs-lookup"><span data-stu-id="9a979-145">How to get operational insights with password management reports</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-get-insights#view-password-reset-activity)




