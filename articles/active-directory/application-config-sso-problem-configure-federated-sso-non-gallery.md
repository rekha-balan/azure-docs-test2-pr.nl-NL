---
title: Problem configuring federated single sign-on for a non-gallery application | Microsoft Docs
description: Address some of the common problems you may encounter when configuring federated single sign-on to your custom SAML application that is not listed in the Azure AD Application Gallery
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 7494607c4f5278b9354c569f073f812ed5cbffc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552085"
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="fbee8-103">Problem configuring federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="fbee8-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="fbee8-104">If you encounter a problem when configuring an application.</span><span class="sxs-lookup"><span data-stu-id="fbee8-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="fbee8-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="fbee8-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="fbee8-106">Can’t add another instance of the application</span><span class="sxs-lookup"><span data-stu-id="fbee8-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="fbee8-107">To add a second instance of an application, you need to be able to:</span><span class="sxs-lookup"><span data-stu-id="fbee8-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="fbee8-108">Configure a unique identifier for the second instance.</span><span class="sxs-lookup"><span data-stu-id="fbee8-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="fbee8-109">You won’t be able to configure the same identifier used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="fbee8-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="fbee8-110">Configure a different certificate than the one used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="fbee8-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="fbee8-111">If the application doesn’t support any of the above.</span><span class="sxs-lookup"><span data-stu-id="fbee8-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="fbee8-112">Then, you won’t be able to configure a second instance.</span><span class="sxs-lookup"><span data-stu-id="fbee8-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="fbee8-113">Where do I set the EntityID (User Identifier) format</span><span class="sxs-lookup"><span data-stu-id="fbee8-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="fbee8-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span><span class="sxs-lookup"><span data-stu-id="fbee8-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="fbee8-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="fbee8-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="fbee8-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="fbee8-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="fbee8-117">Where do I get the application metadata or certificate from Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbee8-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="fbee8-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="fbee8-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="fbee8-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="fbee8-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fbee8-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="fbee8-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbee8-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="fbee8-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbee8-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="fbee8-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbee8-123">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="fbee8-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fbee8-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="fbee8-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fbee8-125">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbee8-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="fbee8-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="fbee8-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fbee8-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="fbee8-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="fbee8-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="fbee8-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="fbee8-129">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="fbee8-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="fbee8-130">The metadata can only be retrieved as a XML file.</span><span class="sxs-lookup"><span data-stu-id="fbee8-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbee8-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbee8-131">Next steps</span></span>
[<span data-ttu-id="fbee8-132">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbee8-132">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
