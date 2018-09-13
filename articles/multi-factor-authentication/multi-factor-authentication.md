---
title: Learn about two-step verification in Azure MFA | Microsoft Docs
description: 'What is Azure Multi-factor Authentication, why use MFA, more information about the Multi-factor Authentication client and the different methods and versions available. '
keywords: introduction to MFA, mfa overview, what is mfa
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: kgremban
ms.openlocfilehash: 4a29c98285ac3e1e21b98d028942ef88533c2f01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554759"
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="4d901-104">What is Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="4d901-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4d901-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span><span class="sxs-lookup"><span data-stu-id="4d901-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="4d901-106">It works by requiring any two or more of the following verification methods:</span><span class="sxs-lookup"><span data-stu-id="4d901-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="4d901-107">Something you know (typically a password)</span><span class="sxs-lookup"><span data-stu-id="4d901-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="4d901-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span><span class="sxs-lookup"><span data-stu-id="4d901-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="4d901-109">Something you are (biometrics)</span><span class="sxs-lookup"><span data-stu-id="4d901-109">Something you are (biometrics)</span></span>

<span data-ttu-id="4d901-110"><center>![Username and Password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="4d901-110"><center>![Username and Password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="4d901-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span><span class="sxs-lookup"><span data-stu-id="4d901-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="4d901-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span><span class="sxs-lookup"><span data-stu-id="4d901-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="4d901-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span><span class="sxs-lookup"><span data-stu-id="4d901-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="4d901-114">Why use Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="4d901-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4d901-115">Today, more than ever, people are increasingly connected.</span><span class="sxs-lookup"><span data-stu-id="4d901-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="4d901-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span><span class="sxs-lookup"><span data-stu-id="4d901-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="4d901-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span><span class="sxs-lookup"><span data-stu-id="4d901-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="4d901-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span><span class="sxs-lookup"><span data-stu-id="4d901-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Easy to Use](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/simple.png) | ![Scalable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/scalable.png) | ![Always Protected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/protected.png) | ![Reliable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="4d901-123">**Easy to use**</span><span class="sxs-lookup"><span data-stu-id="4d901-123">**Easy to use**</span></span> |<span data-ttu-id="4d901-124">**Scalable**</span><span class="sxs-lookup"><span data-stu-id="4d901-124">**Scalable**</span></span> |<span data-ttu-id="4d901-125">**Always Protected**</span><span class="sxs-lookup"><span data-stu-id="4d901-125">**Always Protected**</span></span> |<span data-ttu-id="4d901-126">**Reliable**</span><span class="sxs-lookup"><span data-stu-id="4d901-126">**Reliable**</span></span> |

* <span data-ttu-id="4d901-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span><span class="sxs-lookup"><span data-stu-id="4d901-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="4d901-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span><span class="sxs-lookup"><span data-stu-id="4d901-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="4d901-129">Best of all, in many instances it can be set up with just a few simple clicks.</span><span class="sxs-lookup"><span data-stu-id="4d901-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="4d901-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span><span class="sxs-lookup"><span data-stu-id="4d901-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="4d901-131">This protection is even extended to your high-volume, mission-critical scenarios.</span><span class="sxs-lookup"><span data-stu-id="4d901-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="4d901-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span><span class="sxs-lookup"><span data-stu-id="4d901-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="4d901-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4d901-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="4d901-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span><span class="sxs-lookup"><span data-stu-id="4d901-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="4d901-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d901-135">Next steps</span></span>

- <span data-ttu-id="4d901-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="4d901-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="4d901-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="4d901-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>










