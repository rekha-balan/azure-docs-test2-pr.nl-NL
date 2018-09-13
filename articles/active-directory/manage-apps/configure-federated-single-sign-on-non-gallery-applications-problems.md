---
title: Problem configuring federated single sign-on for a non-gallery application | Microsoft Docs
description: Address some of the common problems you may encounter when configuring federated single sign-on to your custom SAML application that is not listed in the Azure AD Application Gallery
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: ef020e968f88e9976651b5ea22039e42e651db28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865511"
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="69a73-103">Problem configuring federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="69a73-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="69a73-104">If you encounter a problem when configuring an application.</span><span class="sxs-lookup"><span data-stu-id="69a73-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="69a73-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/application-config-sso-how-to-configure-federated-sso-non-gallery)</span><span class="sxs-lookup"><span data-stu-id="69a73-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/application-config-sso-how-to-configure-federated-sso-non-gallery)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="69a73-106">Can’t add another instance of the application</span><span class="sxs-lookup"><span data-stu-id="69a73-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="69a73-107">To add a second instance of an application, you need to be able to:</span><span class="sxs-lookup"><span data-stu-id="69a73-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="69a73-108">Configure a unique identifier for the second instance.</span><span class="sxs-lookup"><span data-stu-id="69a73-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="69a73-109">You cannot configure the same identifier used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="69a73-109">You cannot configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="69a73-110">Configure a different certificate than the one used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="69a73-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="69a73-111">If the application doesn’t support any of the preceding, you cannot configure a second instance.</span><span class="sxs-lookup"><span data-stu-id="69a73-111">If the application doesn’t support any of the preceding, you cannot configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="69a73-112">Where do I set the EntityID (User Identifier) format</span><span class="sxs-lookup"><span data-stu-id="69a73-112">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="69a73-113">You cannot select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span><span class="sxs-lookup"><span data-stu-id="69a73-113">You cannot select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="69a73-114">Azure AD selects the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="69a73-114">Azure AD selects the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="69a73-115">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="69a73-115">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="69a73-116">Where do I get the application metadata or certificate from Azure AD</span><span class="sxs-lookup"><span data-stu-id="69a73-116">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="69a73-117">To download the application metadata or certificate from Azure AD, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="69a73-117">To download the application metadata or certificate from Azure AD, follow these steps:</span></span>

1.  <span data-ttu-id="69a73-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="69a73-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="69a73-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="69a73-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="69a73-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="69a73-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="69a73-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="69a73-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="69a73-122">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="69a73-122">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="69a73-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="69a73-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="69a73-124">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="69a73-124">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="69a73-125">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="69a73-125">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="69a73-126">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="69a73-126">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="69a73-127">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="69a73-127">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="69a73-128">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="69a73-128">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="69a73-129">The metadata can only be retrieved as an XML file.</span><span class="sxs-lookup"><span data-stu-id="69a73-129">The metadata can only be retrieved as an XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="69a73-130">Don't know how to customize SAML claims sent to an application</span><span class="sxs-lookup"><span data-stu-id="69a73-130">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="69a73-131">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span><span class="sxs-lookup"><span data-stu-id="69a73-131">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69a73-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="69a73-132">Next steps</span></span>
[<span data-ttu-id="69a73-133">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69a73-133">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
