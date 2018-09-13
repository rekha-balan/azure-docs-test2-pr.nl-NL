---
title: Two-step verification and AD FS - Azure MFA | Microsoft Docs
description: This is the Azure Multi-Factor authentication page that describes how to get started with Azure MFA and AD FS.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: kgremban
ms.openlocfilehash: b31d3482d3acef19659f81f2930bb8bfdf7b5d9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551107"
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="ed400-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed400-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="ed400-104"><center>![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="ed400-104"><center>![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="ed400-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ed400-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="ed400-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed400-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="ed400-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="ed400-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="ed400-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="ed400-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="ed400-109">Verification Experience - Browse-based Apps</span><span class="sxs-lookup"><span data-stu-id="ed400-109">Verification Experience - Browse-based Apps</span></span> | <span data-ttu-id="ed400-110">Verification Experience - Non-Browser-based Apps</span><span class="sxs-lookup"><span data-stu-id="ed400-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed400-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ed400-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="ed400-112">The first verification step is performed on-premises using AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed400-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="ed400-113">The second step is a phone-based method carried out using cloud authentication.</span><span class="sxs-lookup"><span data-stu-id="ed400-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="ed400-114">Securing Azure AD resources using Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed400-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="ed400-115">The first verification step is performed on-premises using AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed400-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="ed400-116">The second step is performed on-premises by honoring the claim.</span><span class="sxs-lookup"><span data-stu-id="ed400-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="ed400-117">Caveats with app passwords for federated users:</span><span class="sxs-lookup"><span data-stu-id="ed400-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="ed400-118">App passwords are verified using cloud authentication, so they bypass federation.</span><span class="sxs-lookup"><span data-stu-id="ed400-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="ed400-119">Federation is only actively used when setting up an app password.</span><span class="sxs-lookup"><span data-stu-id="ed400-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="ed400-120">On-premises Client Access Control settings are not honored by app passwords.</span><span class="sxs-lookup"><span data-stu-id="ed400-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="ed400-121">You lose on-premises authentication-logging capability for app passwords.</span><span class="sxs-lookup"><span data-stu-id="ed400-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="ed400-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span><span class="sxs-lookup"><span data-stu-id="ed400-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed400-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed400-123">Next steps</span></span>
<span data-ttu-id="ed400-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS see the following articles:</span><span class="sxs-lookup"><span data-stu-id="ed400-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS see the following articles:</span></span>

* [<span data-ttu-id="ed400-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="ed400-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="ed400-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="ed400-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="ed400-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="ed400-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)

