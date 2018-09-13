---
title: Azure Active Directory hybrid identity design considerations - determine content management requirements | Microsoft Docs
description: Provides insight into how to determine the content management requirements of your business. Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses. It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials. Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.
documentationcenter: ''
services: active-directory
author: billmath
manager: femila
editor: ''
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 2c41c96078f8fe75596344ca8f9c54bd3691100b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662170"
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="958df-106">Determine content management requirements for your hybrid identity solution</span><span class="sxs-lookup"><span data-stu-id="958df-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="958df-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span><span class="sxs-lookup"><span data-stu-id="958df-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="958df-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span><span class="sxs-lookup"><span data-stu-id="958df-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="958df-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span><span class="sxs-lookup"><span data-stu-id="958df-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="958df-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="958df-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="958df-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span><span class="sxs-lookup"><span data-stu-id="958df-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="958df-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span><span class="sxs-lookup"><span data-stu-id="958df-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="958df-113">**Security controls that will be leveraging your identity management system**</span><span class="sxs-lookup"><span data-stu-id="958df-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="958df-114">In general, content management requirements will leverage your identity management system in the following areas:</span><span class="sxs-lookup"><span data-stu-id="958df-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="958df-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span><span class="sxs-lookup"><span data-stu-id="958df-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="958df-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span><span class="sxs-lookup"><span data-stu-id="958df-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="958df-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span><span class="sxs-lookup"><span data-stu-id="958df-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="958df-118">This is also important for auditing trail purpose.</span><span class="sxs-lookup"><span data-stu-id="958df-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="958df-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span><span class="sxs-lookup"><span data-stu-id="958df-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="958df-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span><span class="sxs-lookup"><span data-stu-id="958df-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="958df-121">Does your company have security controls in place to enforce data privacy?</span><span class="sxs-lookup"><span data-stu-id="958df-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="958df-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span><span class="sxs-lookup"><span data-stu-id="958df-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="958df-123">Does your company use data classification?</span><span class="sxs-lookup"><span data-stu-id="958df-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="958df-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span><span class="sxs-lookup"><span data-stu-id="958df-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="958df-125">Does your company currently have any solution for data leakage?</span><span class="sxs-lookup"><span data-stu-id="958df-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="958df-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span><span class="sxs-lookup"><span data-stu-id="958df-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="958df-127">Does your company need to audit access to resources?</span><span class="sxs-lookup"><span data-stu-id="958df-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="958df-128">If yes, what type of resources?</span><span class="sxs-lookup"><span data-stu-id="958df-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="958df-129">If yes, what level of information is necessary?</span><span class="sxs-lookup"><span data-stu-id="958df-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="958df-130">If yes, where the audit log must reside?</span><span class="sxs-lookup"><span data-stu-id="958df-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="958df-131">On-premises or in the cloud?</span><span class="sxs-lookup"><span data-stu-id="958df-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="958df-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span><span class="sxs-lookup"><span data-stu-id="958df-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="958df-133">Does your company need to encrypt all documents/contents shared with external business partners?</span><span class="sxs-lookup"><span data-stu-id="958df-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="958df-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span><span class="sxs-lookup"><span data-stu-id="958df-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="958df-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span><span class="sxs-lookup"><span data-stu-id="958df-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="958df-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span><span class="sxs-lookup"><span data-stu-id="958df-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="958df-137">By having answered those questions you will select which option best suits your business needs.</span><span class="sxs-lookup"><span data-stu-id="958df-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="958df-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="958df-138">Next steps</span></span>
[<span data-ttu-id="958df-139">Determine access control requirements</span><span class="sxs-lookup"><span data-stu-id="958df-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="958df-140">See Also</span><span class="sxs-lookup"><span data-stu-id="958df-140">See Also</span></span>
[<span data-ttu-id="958df-141">Design considerations overview</span><span class="sxs-lookup"><span data-stu-id="958df-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)


