---
title: Two-step verification and AD FS - Azure MFA | Microsoft Docs
description: This is the Azure Multi-Factor authentication page that describes how to get started with Azure MFA and AD FS.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 6ce31bba9fb2f237586c6e59cbb5be7643c35aa1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870269"
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="aa44c-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="aa44c-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>

<span data-ttu-id="aa44c-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="aa44c-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="aa44c-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="aa44c-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="aa44c-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="aa44c-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="aa44c-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="aa44c-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="aa44c-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="aa44c-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="aa44c-109">Verification Experience - Browser-based Apps</span><span class="sxs-lookup"><span data-stu-id="aa44c-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="aa44c-110">Verification Experience - Non-Browser-based Apps</span><span class="sxs-lookup"><span data-stu-id="aa44c-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa44c-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="aa44c-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="aa44c-112">The first verification step is performed on-premises using AD FS.</span><span class="sxs-lookup"><span data-stu-id="aa44c-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="aa44c-113">The second step is a phone-based method carried out using cloud authentication.</span><span class="sxs-lookup"><span data-stu-id="aa44c-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="aa44c-114">Securing Azure AD resources using Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="aa44c-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="aa44c-115">The first verification step is performed on-premises using AD FS.</span><span class="sxs-lookup"><span data-stu-id="aa44c-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="aa44c-116">The second step is performed on-premises by honoring the claim.</span><span class="sxs-lookup"><span data-stu-id="aa44c-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="aa44c-117">Caveats with app passwords for federated users:</span><span class="sxs-lookup"><span data-stu-id="aa44c-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="aa44c-118">App passwords are verified using cloud authentication, so they bypass federation.</span><span class="sxs-lookup"><span data-stu-id="aa44c-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="aa44c-119">Federation is only actively used when setting up an app password.</span><span class="sxs-lookup"><span data-stu-id="aa44c-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="aa44c-120">On-premises Client Access Control settings are not honored by app passwords.</span><span class="sxs-lookup"><span data-stu-id="aa44c-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="aa44c-121">You lose on-premises authentication-logging capability for app passwords.</span><span class="sxs-lookup"><span data-stu-id="aa44c-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="aa44c-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span><span class="sxs-lookup"><span data-stu-id="aa44c-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

<span data-ttu-id="aa44c-123">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="aa44c-123">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="aa44c-124">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="aa44c-124">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](howto-mfa-adfs.md)
* [<span data-ttu-id="aa44c-125">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="aa44c-125">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](howto-mfaserver-adfs-2012.md)
* [<span data-ttu-id="aa44c-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="aa44c-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](howto-mfaserver-adfs-2.md)
