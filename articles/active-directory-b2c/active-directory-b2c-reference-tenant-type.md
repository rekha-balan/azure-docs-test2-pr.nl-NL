---
title: 'Azure Active Directory B2C: Region availability & data residency | Microsoft Docs'
description: A topic on the types of Azure Active Directory B2C tenants
services: active-directory-b2c
documentationcenter: ''
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: 0d5919173d358cffe977eefda9340018fef4fc01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551940"
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="69517-103">Azure Active Directory B2C: Region availability & data residency</span><span class="sxs-lookup"><span data-stu-id="69517-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="69517-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span><span class="sxs-lookup"><span data-stu-id="69517-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="69517-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="69517-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="69517-106">Summary</span><span class="sxs-lookup"><span data-stu-id="69517-106">Summary</span></span>
<span data-ttu-id="69517-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span><span class="sxs-lookup"><span data-stu-id="69517-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="69517-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="69517-108">Concepts</span></span>
* <span data-ttu-id="69517-109">**Region availability** refers to where a service is available for use.</span><span class="sxs-lookup"><span data-stu-id="69517-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="69517-110">**Data residency** refers to where user data is stored.</span><span class="sxs-lookup"><span data-stu-id="69517-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="69517-111">Region availability</span><span class="sxs-lookup"><span data-stu-id="69517-111">Region availability</span></span>
<span data-ttu-id="69517-112">Azure AD B2C is available worldwide via the Azure public cloud.</span><span class="sxs-lookup"><span data-stu-id="69517-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="69517-113">This differs from the model most other Azure services follow which couple availability with data residency.</span><span class="sxs-lookup"><span data-stu-id="69517-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="69517-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="69517-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="69517-115">Data residency</span><span class="sxs-lookup"><span data-stu-id="69517-115">Data residency</span></span>
<span data-ttu-id="69517-116">Azure AD B2C stores user data in either United States or Europe.</span><span class="sxs-lookup"><span data-stu-id="69517-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="69517-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="69517-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Screen shot of a preview tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="69517-119">Data resides in the United States for the following countries/regions:</span><span class="sxs-lookup"><span data-stu-id="69517-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="69517-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span><span class="sxs-lookup"><span data-stu-id="69517-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="69517-121">Data resides in Europe for the following countries/regions:</span><span class="sxs-lookup"><span data-stu-id="69517-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="69517-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span><span class="sxs-lookup"><span data-stu-id="69517-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="69517-123">The remaining countries/regions are in the process of being added to the list.</span><span class="sxs-lookup"><span data-stu-id="69517-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="69517-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span><span class="sxs-lookup"><span data-stu-id="69517-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="69517-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span><span class="sxs-lookup"><span data-stu-id="69517-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="69517-126">Preview tenant</span><span class="sxs-lookup"><span data-stu-id="69517-126">Preview tenant</span></span>
<span data-ttu-id="69517-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span><span class="sxs-lookup"><span data-stu-id="69517-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="69517-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span><span class="sxs-lookup"><span data-stu-id="69517-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69517-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="69517-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="69517-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span><span class="sxs-lookup"><span data-stu-id="69517-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="69517-131">You have to create a production-scale B2C tenant with a different domain name.</span><span class="sxs-lookup"><span data-stu-id="69517-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Screen shot of a preview tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)


