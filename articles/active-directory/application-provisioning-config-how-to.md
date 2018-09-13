---
title: How to configure user provisioning to an Azure AD Gallery application | Microsoft Docs
description: How you can quickly configure rich user account provisioning and deprovisioning to applications already listed in the Azure AD Application Gallery
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
ms.openlocfilehash: a666c817fe2b208f8bffb5d8bf8d4aa995618515
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552552"
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="253f0-103">How to configure user provisioning to an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="253f0-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="253f0-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span><span class="sxs-lookup"><span data-stu-id="253f0-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="253f0-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span><span class="sxs-lookup"><span data-stu-id="253f0-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="253f0-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span><span class="sxs-lookup"><span data-stu-id="253f0-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="253f0-107">This can be one of two values:</span><span class="sxs-lookup"><span data-stu-id="253f0-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="253f0-108">Configuring an application for Manual Provisioning</span><span class="sxs-lookup"><span data-stu-id="253f0-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="253f0-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span><span class="sxs-lookup"><span data-stu-id="253f0-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="253f0-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span><span class="sxs-lookup"><span data-stu-id="253f0-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="253f0-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span><span class="sxs-lookup"><span data-stu-id="253f0-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="253f0-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span><span class="sxs-lookup"><span data-stu-id="253f0-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="253f0-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span><span class="sxs-lookup"><span data-stu-id="253f0-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="253f0-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span><span class="sxs-lookup"><span data-stu-id="253f0-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="253f0-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="253f0-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="253f0-116">Configuring an application for Automatic Provisioning</span><span class="sxs-lookup"><span data-stu-id="253f0-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="253f0-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span><span class="sxs-lookup"><span data-stu-id="253f0-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="253f0-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="253f0-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="253f0-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="253f0-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="253f0-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span><span class="sxs-lookup"><span data-stu-id="253f0-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="253f0-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span><span class="sxs-lookup"><span data-stu-id="253f0-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="253f0-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="253f0-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="253f0-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span><span class="sxs-lookup"><span data-stu-id="253f0-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="253f0-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span><span class="sxs-lookup"><span data-stu-id="253f0-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="253f0-125">For more information on this important process.</span><span class="sxs-lookup"><span data-stu-id="253f0-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="253f0-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="253f0-126">Next steps</span></span>
[<span data-ttu-id="253f0-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="253f0-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

