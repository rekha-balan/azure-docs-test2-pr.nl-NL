---
title: Change signature hash algorithm for Office 365 relying party trust | Microsoft Docs
description: This page provides guidelines for changing SHA algorithm for federation trust with Office 365
keywords: SHA1,SHA256,O365,federation,aadconnect,adfs,ad fs,change sha,federation trust,relying party trust
services: active-directory
documentationcenter: ''
author: anandyadavmsft
manager: samueld
editor: ''
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3d803b31b961dfadb334ba8b712c8816f5cf45a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552994"
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="193e0-104">Change signature hash algorithm for Office 365 relying party trust</span><span class="sxs-lookup"><span data-stu-id="193e0-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="193e0-105">Overview</span><span class="sxs-lookup"><span data-stu-id="193e0-105">Overview</span></span>
<span data-ttu-id="193e0-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span><span class="sxs-lookup"><span data-stu-id="193e0-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="193e0-107">This signature can be based on SHA1 or SHA256.</span><span class="sxs-lookup"><span data-stu-id="193e0-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="193e0-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span><span class="sxs-lookup"><span data-stu-id="193e0-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="193e0-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span><span class="sxs-lookup"><span data-stu-id="193e0-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="193e0-110">Change the token-signing algorithm</span><span class="sxs-lookup"><span data-stu-id="193e0-110">Change the token-signing algorithm</span></span>
<span data-ttu-id="193e0-111">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span><span class="sxs-lookup"><span data-stu-id="193e0-111">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="193e0-112">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span><span class="sxs-lookup"><span data-stu-id="193e0-112">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="193e0-113">AD FS management console</span><span class="sxs-lookup"><span data-stu-id="193e0-113">AD FS management console</span></span>
1. <span data-ttu-id="193e0-114">Open the AD FS management console on the primary AD FS server.</span><span class="sxs-lookup"><span data-stu-id="193e0-114">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="193e0-115">Expand the AD FS node and click **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="193e0-115">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="193e0-116">Right-click your Office 365/Azure relying party trust and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="193e0-116">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="193e0-117">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span><span class="sxs-lookup"><span data-stu-id="193e0-117">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="193e0-118">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="193e0-118">Click **OK**.</span></span>

![SHA256 signing algorithm--MMC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="193e0-120">AD FS PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="193e0-120">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="193e0-121">On any AD FS server, open PowerShell under administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="193e0-121">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="193e0-122">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="193e0-122">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="193e0-123">Also read</span><span class="sxs-lookup"><span data-stu-id="193e0-123">Also read</span></span>
* [<span data-ttu-id="193e0-124">Repair Office 365 trust with Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="193e0-124">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)


