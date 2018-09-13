---
title: Automate provisioning of apps using SCIM in Azure Active Directory | Microsoft Docs
description: Azure Active Directory can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the SCIM protocol specification
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: barbkess
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;seohack1
ms.openlocfilehash: 4247ef1ffd1b8d5c5ec393e3ebff20c3e04e32b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867419"
---
# <a name="using-system-for-cross-domain-identity-management-scim-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="9b181-103">Using System for Cross-Domain Identity Management (SCIM) to automatically provision users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="9b181-103">Using System for Cross-Domain Identity Management (SCIM) to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="9b181-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9b181-104">Overview</span></span>
<span data-ttu-id="9b181-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="9b181-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="9b181-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span><span class="sxs-lookup"><span data-stu-id="9b181-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="9b181-107">The web service can then translate those requests into operations on the target identity store.</span><span class="sxs-lookup"><span data-stu-id="9b181-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

<span data-ttu-id="9b181-108">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span><span class="sxs-lookup"><span data-stu-id="9b181-108">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="9b181-109">This capability can be used in conjunction with the “bring your own app” capability in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b181-109">This capability can be used in conjunction with the “bring your own app” capability in Azure AD.</span></span> <span data-ttu-id="9b181-110">This capability enables single sign-on and automatic user provisioning for applications that are fronted by a SCIM web service.</span><span class="sxs-lookup"><span data-stu-id="9b181-110">This capability enables single sign-on and automatic user provisioning for applications that are fronted by a SCIM web service.</span></span>

<span data-ttu-id="9b181-111">There are two use cases for using SCIM in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="9b181-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="9b181-112">**Provisioning users and groups to applications that support SCIM** - Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span><span class="sxs-lookup"><span data-stu-id="9b181-112">**Provisioning users and groups to applications that support SCIM** - Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
  
* <span data-ttu-id="9b181-113">**Building your own provisioning solution for applications that support other API-based provisioning** - For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b181-113">**Building your own provisioning solution for applications that support other API-based provisioning** - For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="9b181-114">To help you develop a SCIM endpoint, there are Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span><span class="sxs-lookup"><span data-stu-id="9b181-114">To help you develop a SCIM endpoint, there are Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="9b181-115">Provisioning users and groups to applications that support SCIM</span><span class="sxs-lookup"><span data-stu-id="9b181-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="9b181-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service, and accept OAuth bearer tokens for authentication.</span><span class="sxs-lookup"><span data-stu-id="9b181-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service, and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="9b181-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span><span class="sxs-lookup"><span data-stu-id="9b181-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="9b181-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="9b181-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="9b181-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="9b181-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="9b181-122">By default, users are queried by externalId and groups are queried by displayName.</span><span class="sxs-lookup"><span data-stu-id="9b181-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="9b181-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="9b181-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="9b181-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="9b181-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="9b181-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span><span class="sxs-lookup"><span data-stu-id="9b181-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="9b181-127">Getting started</span><span class="sxs-lookup"><span data-stu-id="9b181-127">Getting started</span></span>
<span data-ttu-id="9b181-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span><span class="sxs-lookup"><span data-stu-id="9b181-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="9b181-129">Once connected, Azure AD runs a synchronization process every 40 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span><span class="sxs-lookup"><span data-stu-id="9b181-129">Once connected, Azure AD runs a synchronization process every 40 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="9b181-130">**To connect an application that supports SCIM:**</span><span class="sxs-lookup"><span data-stu-id="9b181-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="9b181-131">Sign in to [the Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b181-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="9b181-132">Browse to **Azure Active Directory > Enterprise Applications**, and select **New application > All > Non-gallery application**.</span><span class="sxs-lookup"><span data-stu-id="9b181-132">Browse to **Azure Active Directory > Enterprise Applications**, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="9b181-133">Enter a name for your application, and click **Add** icon to create an app object.</span><span class="sxs-lookup"><span data-stu-id="9b181-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="9b181-134">![][1]
  *Figure 2: Azure AD application gallery*</span><span class="sxs-lookup"><span data-stu-id="9b181-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="9b181-135">In the resulting screen, select the **Provisioning** tab in the left column.</span><span class="sxs-lookup"><span data-stu-id="9b181-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="9b181-136">In the **Provisioning Mode** menu, select **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="9b181-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="9b181-137">![][2]
  *Figure 3: Configuring provisioning in the Azure portal*</span><span class="sxs-lookup"><span data-stu-id="9b181-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="9b181-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="9b181-139">Example: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="9b181-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="9b181-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span><span class="sxs-lookup"><span data-stu-id="9b181-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="9b181-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span><span class="sxs-lookup"><span data-stu-id="9b181-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="9b181-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span><span class="sxs-lookup"><span data-stu-id="9b181-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="9b181-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="9b181-144">If the attempts fail, error information is displayed.</span><span class="sxs-lookup"><span data-stu-id="9b181-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="9b181-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span><span class="sxs-lookup"><span data-stu-id="9b181-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="9b181-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span><span class="sxs-lookup"><span data-stu-id="9b181-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="9b181-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span><span class="sxs-lookup"><span data-stu-id="9b181-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="9b181-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span><span class="sxs-lookup"><span data-stu-id="9b181-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="9b181-149">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="9b181-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9b181-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span><span class="sxs-lookup"><span data-stu-id="9b181-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="9b181-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span><span class="sxs-lookup"><span data-stu-id="9b181-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="9b181-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span><span class="sxs-lookup"><span data-stu-id="9b181-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="9b181-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="9b181-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="9b181-154">Click **Save** to start the Azure AD provisioning service.</span><span class="sxs-lookup"><span data-stu-id="9b181-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="9b181-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span><span class="sxs-lookup"><span data-stu-id="9b181-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="9b181-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span><span class="sxs-lookup"><span data-stu-id="9b181-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="9b181-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9b181-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](check-status-user-account-provisioning.md).</span></span>

>[!NOTE]
><span data-ttu-id="9b181-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="9b181-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="9b181-159">Building your own provisioning solution for any application</span><span class="sxs-lookup"><span data-stu-id="9b181-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="9b181-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span><span class="sxs-lookup"><span data-stu-id="9b181-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="9b181-161">Here’s how it works:</span><span class="sxs-lookup"><span data-stu-id="9b181-161">Here’s how it works:</span></span>

1. <span data-ttu-id="9b181-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="9b181-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="9b181-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span><span class="sxs-lookup"><span data-stu-id="9b181-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="9b181-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span><span class="sxs-lookup"><span data-stu-id="9b181-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="9b181-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="9b181-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="9b181-166">Users and groups are assigned to this application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b181-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="9b181-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span><span class="sxs-lookup"><span data-stu-id="9b181-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="9b181-168">The synchronization process handling the queue runs every 40 minutes.</span><span class="sxs-lookup"><span data-stu-id="9b181-168">The synchronization process handling the queue runs every 40 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="9b181-169">Code Samples</span><span class="sxs-lookup"><span data-stu-id="9b181-169">Code Samples</span></span>
<span data-ttu-id="9b181-170">To make this process easier, [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span><span class="sxs-lookup"><span data-stu-id="9b181-170">To make this process easier, [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="9b181-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span><span class="sxs-lookup"><span data-stu-id="9b181-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="9b181-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span><span class="sxs-lookup"><span data-stu-id="9b181-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="9b181-173">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="9b181-173">**Prerequisites**</span></span>

* <span data-ttu-id="9b181-174">Visual Studio 2013 or later</span><span class="sxs-lookup"><span data-stu-id="9b181-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="9b181-175">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="9b181-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="9b181-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="9b181-177">This machine must be accessible from the cloud</span><span class="sxs-lookup"><span data-stu-id="9b181-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="9b181-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="9b181-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)

### <a name="getting-started"></a><span data-ttu-id="9b181-179">Getting Started</span><span class="sxs-lookup"><span data-stu-id="9b181-179">Getting Started</span></span>
<span data-ttu-id="9b181-180">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="9b181-180">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="9b181-181">**To create a sample SCIM endpoint:**</span><span class="sxs-lookup"><span data-stu-id="9b181-181">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="9b181-182">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="9b181-182">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="9b181-183">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="9b181-183">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="9b181-184">In this folder, launch the FileProvisioning\Host\FileProvisioningService.csproj project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b181-184">In this folder, launch the FileProvisioning\Host\FileProvisioningService.csproj project in Visual Studio.</span></span>
4. <span data-ttu-id="9b181-185">Select **Tools > NuGet Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningService project to resolve the solution references:</span><span class="sxs-lookup"><span data-stu-id="9b181-185">Select **Tools > NuGet Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningService project to resolve the solution references:</span></span>
  ```` 
   Update-Package -Reinstall
  ````
5. <span data-ttu-id="9b181-186">Build the FileProvisioningService project.</span><span class="sxs-lookup"><span data-stu-id="9b181-186">Build the FileProvisioningService project.</span></span>
6. <span data-ttu-id="9b181-187">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\FileProvisioning\Host\bin\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="9b181-187">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\FileProvisioning\Host\bin\Debug** folder.</span></span>
7. <span data-ttu-id="9b181-188">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span><span class="sxs-lookup"><span data-stu-id="9b181-188">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileSvc.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="9b181-189">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span><span class="sxs-lookup"><span data-stu-id="9b181-189">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="9b181-190">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span><span class="sxs-lookup"><span data-stu-id="9b181-190">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="9b181-191">This configuration is required for Azure AD to be able to access this endpoint in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9b181-191">This configuration is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="9b181-192">**To register the sample SCIM endpoint in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9b181-192">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="9b181-193">Sign in to [the Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b181-193">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="9b181-194">Browse to **Azure Active Directory > Enterprise Applications**, and select **New application > All > Non-gallery application**.</span><span class="sxs-lookup"><span data-stu-id="9b181-194">Browse to **Azure Active Directory > Enterprise Applications**, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="9b181-195">Enter a name for your application, and click **Add** icon to create an app object.</span><span class="sxs-lookup"><span data-stu-id="9b181-195">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="9b181-196">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-196">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="9b181-197">In the resulting screen, select the **Provisioning** tab in the left column.</span><span class="sxs-lookup"><span data-stu-id="9b181-197">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="9b181-198">In the **Provisioning Mode** menu, select **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="9b181-198">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="9b181-199">![][2]
  *Figure 4: Configuring provisioning in the Azure portal*</span><span class="sxs-lookup"><span data-stu-id="9b181-199">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="9b181-200">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-200">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="9b181-201">The entry is something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span><span class="sxs-lookup"><span data-stu-id="9b181-201">The entry is something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="9b181-202">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span><span class="sxs-lookup"><span data-stu-id="9b181-202">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="9b181-203">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span><span class="sxs-lookup"><span data-stu-id="9b181-203">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="9b181-204">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span><span class="sxs-lookup"><span data-stu-id="9b181-204">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="9b181-205">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b181-205">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="9b181-206">If the attempts fail, error information is displayed.</span><span class="sxs-lookup"><span data-stu-id="9b181-206">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="9b181-207">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span><span class="sxs-lookup"><span data-stu-id="9b181-207">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="9b181-208">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span><span class="sxs-lookup"><span data-stu-id="9b181-208">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="9b181-209">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span><span class="sxs-lookup"><span data-stu-id="9b181-209">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="9b181-210">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span><span class="sxs-lookup"><span data-stu-id="9b181-210">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="9b181-211">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="9b181-211">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="9b181-212">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span><span class="sxs-lookup"><span data-stu-id="9b181-212">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="9b181-213">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span><span class="sxs-lookup"><span data-stu-id="9b181-213">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="9b181-214">Once your configuration is complete, change the **Provisioning Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="9b181-214">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="9b181-215">Click **Save** to start the Azure AD provisioning service.</span><span class="sxs-lookup"><span data-stu-id="9b181-215">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="9b181-216">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span><span class="sxs-lookup"><span data-stu-id="9b181-216">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="9b181-217">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span><span class="sxs-lookup"><span data-stu-id="9b181-217">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="9b181-218">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9b181-218">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](check-status-user-account-provisioning.md).</span></span>

<span data-ttu-id="9b181-219">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="9b181-219">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="9b181-220">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span><span class="sxs-lookup"><span data-stu-id="9b181-220">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="9b181-221">Development libraries</span><span class="sxs-lookup"><span data-stu-id="9b181-221">Development libraries</span></span>
<span data-ttu-id="9b181-222">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span><span class="sxs-lookup"><span data-stu-id="9b181-222">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="9b181-223">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span><span class="sxs-lookup"><span data-stu-id="9b181-223">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="9b181-224">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-224">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="9b181-225">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span><span class="sxs-lookup"><span data-stu-id="9b181-225">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="9b181-226">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span><span class="sxs-lookup"><span data-stu-id="9b181-226">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="9b181-227">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span><span class="sxs-lookup"><span data-stu-id="9b181-227">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="9b181-228">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span><span class="sxs-lookup"><span data-stu-id="9b181-228">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="9b181-229">Building a Custom SCIM Endpoint</span><span class="sxs-lookup"><span data-stu-id="9b181-229">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="9b181-230">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="9b181-230">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="9b181-231">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="9b181-231">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="9b181-232">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following names:</span><span class="sxs-lookup"><span data-stu-id="9b181-232">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following names:</span></span> 

* <span data-ttu-id="9b181-233">CNNIC</span><span class="sxs-lookup"><span data-stu-id="9b181-233">CNNIC</span></span>
* <span data-ttu-id="9b181-234">Comodo</span><span class="sxs-lookup"><span data-stu-id="9b181-234">Comodo</span></span>
* <span data-ttu-id="9b181-235">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="9b181-235">CyberTrust</span></span>
* <span data-ttu-id="9b181-236">DigiCert</span><span class="sxs-lookup"><span data-stu-id="9b181-236">DigiCert</span></span>
* <span data-ttu-id="9b181-237">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="9b181-237">GeoTrust</span></span>
* <span data-ttu-id="9b181-238">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="9b181-238">GlobalSign</span></span>
* <span data-ttu-id="9b181-239">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="9b181-239">Go Daddy</span></span>
* <span data-ttu-id="9b181-240">VeriSign</span><span class="sxs-lookup"><span data-stu-id="9b181-240">VeriSign</span></span>
* <span data-ttu-id="9b181-241">WoSign</span><span class="sxs-lookup"><span data-stu-id="9b181-241">WoSign</span></span>

<span data-ttu-id="9b181-242">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span><span class="sxs-lookup"><span data-stu-id="9b181-242">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="9b181-243">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="9b181-243">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="9b181-244">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span><span class="sxs-lookup"><span data-stu-id="9b181-244">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="9b181-245">Here is a sample of such a class:</span><span class="sxs-lookup"><span data-stu-id="9b181-245">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="9b181-246">Handling endpoint authentication</span><span class="sxs-lookup"><span data-stu-id="9b181-246">Handling endpoint authentication</span></span>
<span data-ttu-id="9b181-247">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span><span class="sxs-lookup"><span data-stu-id="9b181-247">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="9b181-248">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span><span class="sxs-lookup"><span data-stu-id="9b181-248">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="9b181-249">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="9b181-249">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="9b181-250">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span><span class="sxs-lookup"><span data-stu-id="9b181-250">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="9b181-251">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span><span class="sxs-lookup"><span data-stu-id="9b181-251">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="9b181-252">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span><span class="sxs-lookup"><span data-stu-id="9b181-252">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="9b181-253">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span><span class="sxs-lookup"><span data-stu-id="9b181-253">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="9b181-254">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span><span class="sxs-lookup"><span data-stu-id="9b181-254">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="9b181-255">User and group schema</span><span class="sxs-lookup"><span data-stu-id="9b181-255">User and group schema</span></span>
<span data-ttu-id="9b181-256">Azure Active Directory can provision two types of resources to SCIM web services.</span><span class="sxs-lookup"><span data-stu-id="9b181-256">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="9b181-257">Those types of resources are users and groups.</span><span class="sxs-lookup"><span data-stu-id="9b181-257">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="9b181-258">User resources are identified by the schema identifier, "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User", which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="9b181-258">User resources are identified by the schema identifier, "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User", which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="9b181-259">The default mapping of the attributes of users in Azure Active Directory to the attributes of "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User" resources is provided in table 1, below.</span><span class="sxs-lookup"><span data-stu-id="9b181-259">The default mapping of the attributes of users in Azure Active Directory to the attributes of "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User" resources is provided in table 1, below.</span></span>  

<span data-ttu-id="9b181-260">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="9b181-260">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="9b181-261">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span><span class="sxs-lookup"><span data-stu-id="9b181-261">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="9b181-262">Table 1: Default user attribute mapping</span><span class="sxs-lookup"><span data-stu-id="9b181-262">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="9b181-263">Azure Active Directory user</span><span class="sxs-lookup"><span data-stu-id="9b181-263">Azure Active Directory user</span></span> | <span data-ttu-id="9b181-264">"urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="9b181-264">"urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span> |
| --- | --- |
| <span data-ttu-id="9b181-265">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="9b181-265">IsSoftDeleted</span></span> |<span data-ttu-id="9b181-266">active</span><span class="sxs-lookup"><span data-stu-id="9b181-266">active</span></span> |
| <span data-ttu-id="9b181-267">displayName</span><span class="sxs-lookup"><span data-stu-id="9b181-267">displayName</span></span> |<span data-ttu-id="9b181-268">displayName</span><span class="sxs-lookup"><span data-stu-id="9b181-268">displayName</span></span> |
| <span data-ttu-id="9b181-269">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="9b181-269">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="9b181-270">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="9b181-270">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="9b181-271">givenName</span><span class="sxs-lookup"><span data-stu-id="9b181-271">givenName</span></span> |<span data-ttu-id="9b181-272">name.givenName</span><span class="sxs-lookup"><span data-stu-id="9b181-272">name.givenName</span></span> |
| <span data-ttu-id="9b181-273">jobTitle</span><span class="sxs-lookup"><span data-stu-id="9b181-273">jobTitle</span></span> |<span data-ttu-id="9b181-274">title</span><span class="sxs-lookup"><span data-stu-id="9b181-274">title</span></span> |
| <span data-ttu-id="9b181-275">mail</span><span class="sxs-lookup"><span data-stu-id="9b181-275">mail</span></span> |<span data-ttu-id="9b181-276">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="9b181-276">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="9b181-277">mailNickname</span><span class="sxs-lookup"><span data-stu-id="9b181-277">mailNickname</span></span> |<span data-ttu-id="9b181-278">externalId</span><span class="sxs-lookup"><span data-stu-id="9b181-278">externalId</span></span> |
| <span data-ttu-id="9b181-279">manager</span><span class="sxs-lookup"><span data-stu-id="9b181-279">manager</span></span> |<span data-ttu-id="9b181-280">manager</span><span class="sxs-lookup"><span data-stu-id="9b181-280">manager</span></span> |
| <span data-ttu-id="9b181-281">mobile</span><span class="sxs-lookup"><span data-stu-id="9b181-281">mobile</span></span> |<span data-ttu-id="9b181-282">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="9b181-282">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="9b181-283">objectId</span><span class="sxs-lookup"><span data-stu-id="9b181-283">objectId</span></span> |<span data-ttu-id="9b181-284">ID</span><span class="sxs-lookup"><span data-stu-id="9b181-284">ID</span></span> |
| <span data-ttu-id="9b181-285">postalCode</span><span class="sxs-lookup"><span data-stu-id="9b181-285">postalCode</span></span> |<span data-ttu-id="9b181-286">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="9b181-286">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="9b181-287">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="9b181-287">proxy-Addresses</span></span> |<span data-ttu-id="9b181-288">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="9b181-288">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="9b181-289">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="9b181-289">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="9b181-290">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="9b181-290">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="9b181-291">streetAddress</span><span class="sxs-lookup"><span data-stu-id="9b181-291">streetAddress</span></span> |<span data-ttu-id="9b181-292">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="9b181-292">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="9b181-293">surname</span><span class="sxs-lookup"><span data-stu-id="9b181-293">surname</span></span> |<span data-ttu-id="9b181-294">name.familyName</span><span class="sxs-lookup"><span data-stu-id="9b181-294">name.familyName</span></span> |
| <span data-ttu-id="9b181-295">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="9b181-295">telephone-Number</span></span> |<span data-ttu-id="9b181-296">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="9b181-296">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="9b181-297">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="9b181-297">user-PrincipalName</span></span> |<span data-ttu-id="9b181-298">userName</span><span class="sxs-lookup"><span data-stu-id="9b181-298">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="9b181-299">Table 2: Default group attribute mapping</span><span class="sxs-lookup"><span data-stu-id="9b181-299">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="9b181-300">Azure Active Directory group</span><span class="sxs-lookup"><span data-stu-id="9b181-300">Azure Active Directory group</span></span> | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| <span data-ttu-id="9b181-301">displayName</span><span class="sxs-lookup"><span data-stu-id="9b181-301">displayName</span></span> |<span data-ttu-id="9b181-302">externalId</span><span class="sxs-lookup"><span data-stu-id="9b181-302">externalId</span></span> |
| <span data-ttu-id="9b181-303">mail</span><span class="sxs-lookup"><span data-stu-id="9b181-303">mail</span></span> |<span data-ttu-id="9b181-304">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="9b181-304">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="9b181-305">mailNickname</span><span class="sxs-lookup"><span data-stu-id="9b181-305">mailNickname</span></span> |<span data-ttu-id="9b181-306">displayName</span><span class="sxs-lookup"><span data-stu-id="9b181-306">displayName</span></span> |
| <span data-ttu-id="9b181-307">members</span><span class="sxs-lookup"><span data-stu-id="9b181-307">members</span></span> |<span data-ttu-id="9b181-308">members</span><span class="sxs-lookup"><span data-stu-id="9b181-308">members</span></span> |
| <span data-ttu-id="9b181-309">objectId</span><span class="sxs-lookup"><span data-stu-id="9b181-309">objectId</span></span> |<span data-ttu-id="9b181-310">ID</span><span class="sxs-lookup"><span data-stu-id="9b181-310">ID</span></span> |
| <span data-ttu-id="9b181-311">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="9b181-311">proxyAddresses</span></span> |<span data-ttu-id="9b181-312">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="9b181-312">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="9b181-313">User provisioning and de-provisioning</span><span class="sxs-lookup"><span data-stu-id="9b181-313">User provisioning and de-provisioning</span></span>
<span data-ttu-id="9b181-314">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span><span class="sxs-lookup"><span data-stu-id="9b181-314">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="9b181-315">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-315">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="9b181-316">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span><span class="sxs-lookup"><span data-stu-id="9b181-316">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="9b181-317">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b181-317">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="9b181-318">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="9b181-318">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="9b181-319">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-319">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="9b181-320">Here is the signature of that method:</span><span class="sxs-lookup"><span data-stu-id="9b181-320">Here is the signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="9b181-321">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span><span class="sxs-lookup"><span data-stu-id="9b181-321">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="9b181-322">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span><span class="sxs-lookup"><span data-stu-id="9b181-322">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="9b181-323">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="9b181-323">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="9b181-324">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="9b181-324">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="9b181-325">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="9b181-325">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="9b181-326">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="9b181-326">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="9b181-327">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="9b181-327">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="9b181-328">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b181-328">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="9b181-329">Here is an example of such a request:</span><span class="sxs-lookup"><span data-stu-id="9b181-329">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/scim+json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="9b181-330">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-330">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="9b181-331">The Create method has this signature:</span><span class="sxs-lookup"><span data-stu-id="9b181-331">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="9b181-332">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="9b181-332">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="9b181-333">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span><span class="sxs-lookup"><span data-stu-id="9b181-333">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="9b181-334">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="9b181-334">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="9b181-335">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span><span class="sxs-lookup"><span data-stu-id="9b181-335">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="9b181-336">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span><span class="sxs-lookup"><span data-stu-id="9b181-336">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="9b181-337">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-337">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="9b181-338">Here is the signature of the Retrieve method:</span><span class="sxs-lookup"><span data-stu-id="9b181-338">Here is the signature of the Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="9b181-339">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span><span class="sxs-lookup"><span data-stu-id="9b181-339">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="9b181-340">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="9b181-340">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="9b181-341">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="9b181-341">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="9b181-342">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b181-342">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="9b181-343">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span><span class="sxs-lookup"><span data-stu-id="9b181-343">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="9b181-344">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span><span class="sxs-lookup"><span data-stu-id="9b181-344">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="9b181-345">The value of the attributes query parameter, "ID", signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with an "urn:ietf:params:scim:schemas:core:2.0:User" or "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User" resource, including only the value of that resource’s "ID" attribute.</span><span class="sxs-lookup"><span data-stu-id="9b181-345">The value of the attributes query parameter, "ID", signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with an "urn:ietf:params:scim:schemas:core:2.0:User" or "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User" resource, including only the value of that resource’s "ID" attribute.</span></span>  <span data-ttu-id="9b181-346">The value of the **ID** attribute is known to the requestor.</span><span class="sxs-lookup"><span data-stu-id="9b181-346">The value of the **ID** attribute is known to the requestor.</span></span> <span data-ttu-id="9b181-347">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span><span class="sxs-lookup"><span data-stu-id="9b181-347">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="9b181-348">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-348">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="9b181-349">The value of the properties of the object provided as the value of the parameters argument are as follows:</span><span class="sxs-lookup"><span data-stu-id="9b181-349">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="9b181-350">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="9b181-350">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="9b181-351">parameters.AlternateFilters.ElementAt(x).AttributePath: "ID"</span><span class="sxs-lookup"><span data-stu-id="9b181-351">parameters.AlternateFilters.ElementAt(x).AttributePath: "ID"</span></span>
  * <span data-ttu-id="9b181-352">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="9b181-352">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="9b181-353">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="9b181-353">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="9b181-354">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="9b181-354">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="9b181-355">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="9b181-355">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="9b181-356">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="9b181-356">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="9b181-357">parameters.RequestedAttributePaths.ElementAt(0): "ID"</span><span class="sxs-lookup"><span data-stu-id="9b181-357">parameters.RequestedAttributePaths.ElementAt(0): "ID"</span></span>
  * <span data-ttu-id="9b181-358">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="9b181-358">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="9b181-359">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span><span class="sxs-lookup"><span data-stu-id="9b181-359">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="9b181-360">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span><span class="sxs-lookup"><span data-stu-id="9b181-360">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/scim+json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="9b181-361">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-361">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="9b181-362">Here is the signature of the Update method:</span><span class="sxs-lookup"><span data-stu-id="9b181-362">Here is the signature of the Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="9b181-363">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span><span class="sxs-lookup"><span data-stu-id="9b181-363">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="9b181-364">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="9b181-364">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="9b181-365">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="9b181-365">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="9b181-366">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="9b181-366">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="9b181-367">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="9b181-367">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="9b181-368">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="9b181-368">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="9b181-369">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="9b181-369">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="9b181-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="9b181-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="9b181-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="9b181-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="9b181-372">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span><span class="sxs-lookup"><span data-stu-id="9b181-372">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="9b181-373">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="9b181-373">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="9b181-374">That method has this signature:</span><span class="sxs-lookup"><span data-stu-id="9b181-374">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="9b181-375">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span><span class="sxs-lookup"><span data-stu-id="9b181-375">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="9b181-376">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="9b181-376">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="9b181-377">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="9b181-377">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="9b181-378">Group provisioning and de-provisioning</span><span class="sxs-lookup"><span data-stu-id="9b181-378">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="9b181-379">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span><span class="sxs-lookup"><span data-stu-id="9b181-379">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="9b181-380">Those messages differ from the messages pertaining to users in three ways:</span><span class="sxs-lookup"><span data-stu-id="9b181-380">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="9b181-381">The schema of a group resource is identified as `http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group`.</span><span class="sxs-lookup"><span data-stu-id="9b181-381">The schema of a group resource is identified as `http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group`.</span></span>  
* <span data-ttu-id="9b181-382">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span><span class="sxs-lookup"><span data-stu-id="9b181-382">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="9b181-383">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span><span class="sxs-lookup"><span data-stu-id="9b181-383">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="9b181-384">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span><span class="sxs-lookup"><span data-stu-id="9b181-384">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="9b181-385">Related articles</span><span class="sxs-lookup"><span data-stu-id="9b181-385">Related articles</span></span>
* [<span data-ttu-id="9b181-386">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b181-386">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="9b181-387">Automate User Provisioning/Deprovisioning to SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="9b181-387">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](user-provisioning.md)
* [<span data-ttu-id="9b181-388">Customizing Attribute Mappings for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="9b181-388">Customizing Attribute Mappings for User Provisioning</span></span>](customize-application-attributes.md)
* [<span data-ttu-id="9b181-389">Writing Expressions for Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="9b181-389">Writing Expressions for Attribute Mappings</span></span>](functions-for-customizing-application-data.md)
* [<span data-ttu-id="9b181-390">Scoping Filters for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="9b181-390">Scoping Filters for User Provisioning</span></span>](define-conditional-rules-for-provisioning-user-accounts.md)
* [<span data-ttu-id="9b181-391">Account Provisioning Notifications</span><span class="sxs-lookup"><span data-stu-id="9b181-391">Account Provisioning Notifications</span></span>](user-provisioning.md)
* [<span data-ttu-id="9b181-392">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="9b181-392">List of Tutorials on How to Integrate SaaS Apps</span></span>](../saas-apps/tutorial-list.md)

<!--Image references-->
[0]: ./media/use-scim-to-provision-users-and-groups/scim-figure-1.png
[1]: ./media/use-scim-to-provision-users-and-groups/scim-figure-2a.png
[2]: ./media/use-scim-to-provision-users-and-groups/scim-figure-2b.png
[3]: ./media/use-scim-to-provision-users-and-groups/scim-figure-3.png
[4]: ./media/use-scim-to-provision-users-and-groups/scim-figure-4.png
[5]: ./media/use-scim-to-provision-users-and-groups/scim-figure-5.png
