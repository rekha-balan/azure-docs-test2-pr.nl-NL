---
title: Unlicensed Usage Report | Microsoft Docs
description: The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: ee6106b43f2b90d5033c474896f07a3bab86bf98
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563132"
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="4684b-103">Unlicensed usage report</span><span class="sxs-lookup"><span data-stu-id="4684b-103">Unlicensed usage report</span></span>
<span data-ttu-id="4684b-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span><span class="sxs-lookup"><span data-stu-id="4684b-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="4684b-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span><span class="sxs-lookup"><span data-stu-id="4684b-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="4684b-106">The report shows active usage of the paid features in the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="4684b-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="4684b-107">Report structure</span><span class="sxs-lookup"><span data-stu-id="4684b-107">Report structure</span></span>
| <span data-ttu-id="4684b-108">Column name</span><span class="sxs-lookup"><span data-stu-id="4684b-108">Column name</span></span> | <span data-ttu-id="4684b-109">Description</span><span class="sxs-lookup"><span data-stu-id="4684b-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4684b-110">Unlicensed User</span><span class="sxs-lookup"><span data-stu-id="4684b-110">Unlicensed User</span></span> |<span data-ttu-id="4684b-111">Name of the user</span><span class="sxs-lookup"><span data-stu-id="4684b-111">Name of the user</span></span> |
| <span data-ttu-id="4684b-112">Feature</span><span class="sxs-lookup"><span data-stu-id="4684b-112">Feature</span></span> |<span data-ttu-id="4684b-113">The feature name.</span><span class="sxs-lookup"><span data-stu-id="4684b-113">The feature name.</span></span> <span data-ttu-id="4684b-114">For example: conditional access</span><span class="sxs-lookup"><span data-stu-id="4684b-114">For example: conditional access</span></span> |
| <span data-ttu-id="4684b-115">Application Accessed</span><span class="sxs-lookup"><span data-stu-id="4684b-115">Application Accessed</span></span> |<span data-ttu-id="4684b-116">The name of the application that is being accessed with the feature.</span><span class="sxs-lookup"><span data-stu-id="4684b-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="4684b-117">For example: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4684b-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="4684b-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="4684b-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="4684b-119">Conditional access feature</span><span class="sxs-lookup"><span data-stu-id="4684b-119">Conditional access feature</span></span>
<span data-ttu-id="4684b-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span><span class="sxs-lookup"><span data-stu-id="4684b-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="4684b-121">This applies to MFA / Location policies as well as device polices that use Intune.</span><span class="sxs-lookup"><span data-stu-id="4684b-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="4684b-122">See also</span><span class="sxs-lookup"><span data-stu-id="4684b-122">See also</span></span>
* [<span data-ttu-id="4684b-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span><span class="sxs-lookup"><span data-stu-id="4684b-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="4684b-124">Getting started with conditional access to Azure AD</span><span class="sxs-lookup"><span data-stu-id="4684b-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

