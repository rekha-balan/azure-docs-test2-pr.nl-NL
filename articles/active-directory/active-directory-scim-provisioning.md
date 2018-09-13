---
title: Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications | Microsoft Docs
description: Azure Active Directory can automatically provision users and groups to any application or identity store that is fronted by a Web service with the interface defined in the SCIM protocol specification
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: asmalser
ms.openlocfilehash: 4216b5aa69e29e03ff16d3357072f9af5ec1c69b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555626"
---
# <a name="using-scim-to-enable-automatic-provisioning-of-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="42836-103">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="42836-103">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>
## <a name="overview"></a><span data-ttu-id="42836-104">Overview</span><span class="sxs-lookup"><span data-stu-id="42836-104">Overview</span></span>
<span data-ttu-id="42836-105">Azure Active Directory can automatically provision users and groups to any application or identity store that is fronted by a Web service with the interface defined in the [SCIM 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="42836-105">Azure Active Directory can automatically provision users and groups to any application or identity store that is fronted by a Web service with the interface defined in the [SCIM 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="42836-106">Azure Active Directory can send requests to create, modify and delete assigned users and groups to this Web service, which can then translate those requests into operations upon the target identity store.</span><span class="sxs-lookup"><span data-stu-id="42836-106">Azure Active Directory can send requests to create, modify and delete assigned users and groups to this Web service, which can then translate those requests into operations upon the target identity store.</span></span> 

<span data-ttu-id="42836-107">![][1]
*Figure: Provisioning from Azure Active Directory to an identity store via a Web service*</span><span class="sxs-lookup"><span data-stu-id="42836-107">![][1]
*Figure: Provisioning from Azure Active Directory to an identity store via a Web service*</span></span>

<span data-ttu-id="42836-108">This capability can be used in conjunction with the “[bring your own app](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span><span class="sxs-lookup"><span data-stu-id="42836-108">This capability can be used in conjunction with the “[bring your own app](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="42836-109">There are two use cases for SCIM in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="42836-109">There are two use cases for SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="42836-110">**Provisioning users and groups to applications that support SCIM** - Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication will work with Azure AD of the box.</span><span class="sxs-lookup"><span data-stu-id="42836-110">**Provisioning users and groups to applications that support SCIM** - Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication will work with Azure AD of the box.</span></span>
* <span data-ttu-id="42836-111">**Build your own provisioning solution for applications that support other API-based provisioning** - For non-SCIM applications, you can create a SCIM endpoint to translate between Azure AD’s SCIM endpoint and whatever API the application supports for user provisioning.</span><span class="sxs-lookup"><span data-stu-id="42836-111">**Build your own provisioning solution for applications that support other API-based provisioning** - For non-SCIM applications, you can create a SCIM endpoint to translate between Azure AD’s SCIM endpoint and whatever API the application supports for user provisioning.</span></span>  <span data-ttu-id="42836-112">To aid in the development of a SCIM endpoint, we provide CLI libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span><span class="sxs-lookup"><span data-stu-id="42836-112">To aid in the development of a SCIM endpoint, we provide CLI libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="42836-113">Provisioning Users and Groups To Applications That Support SCIM</span><span class="sxs-lookup"><span data-stu-id="42836-113">Provisioning Users and Groups To Applications That Support SCIM</span></span>
<span data-ttu-id="42836-114">Azure Active Directory can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) Web service and accept OAuth bearer tokens for authentication.</span><span class="sxs-lookup"><span data-stu-id="42836-114">Azure Active Directory can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) Web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="42836-115">Within the SCIM 2.0 specification, applications must meet these requirements:</span><span class="sxs-lookup"><span data-stu-id="42836-115">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="42836-116">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-116">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="42836-117">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-117">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="42836-118">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-118">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="42836-119">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-119">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="42836-120">By default, users are queried by externalId and groups are queried by displayName.</span><span class="sxs-lookup"><span data-stu-id="42836-120">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="42836-121">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-121">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="42836-122">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-122">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="42836-123">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span><span class="sxs-lookup"><span data-stu-id="42836-123">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="42836-124">You should check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span><span class="sxs-lookup"><span data-stu-id="42836-124">You should check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="42836-125">Getting Started</span><span class="sxs-lookup"><span data-stu-id="42836-125">Getting Started</span></span>
<span data-ttu-id="42836-126">Applications that support the SCIM profile described above can be connected to Azure Active Directory using the "custom" app feature in the Azure AD application gallery.</span><span class="sxs-lookup"><span data-stu-id="42836-126">Applications that support the SCIM profile described above can be connected to Azure Active Directory using the "custom" app feature in the Azure AD application gallery.</span></span> <span data-ttu-id="42836-127">Once connected, Azure AD runs a synchronization process every 5 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span><span class="sxs-lookup"><span data-stu-id="42836-127">Once connected, Azure AD runs a synchronization process every 5 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="42836-128">**To connect an application that supports SCIM:**</span><span class="sxs-lookup"><span data-stu-id="42836-128">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="42836-129">In a web browser, launch the Azure management portal at https://manage.windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="42836-129">In a web browser, launch the Azure management portal at https://manage.windowsazure.com.</span></span>
2. <span data-ttu-id="42836-130">Browse to **Active Directory > Directory > [Your Directory] > Applications**, and select **Add > Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="42836-130">Browse to **Active Directory > Directory > [Your Directory] > Applications**, and select **Add > Add an application from the gallery**.</span></span>
3. <span data-ttu-id="42836-131">Select the **Custom** tab on the left, enter a name for your application, and click the checkmark icon to create an app object.</span><span class="sxs-lookup"><span data-stu-id="42836-131">Select the **Custom** tab on the left, enter a name for your application, and click the checkmark icon to create an app object.</span></span>

![][2]

1. <span data-ttu-id="42836-132">In the resulting screen, select the second **Configure account provisioning** button.</span><span class="sxs-lookup"><span data-stu-id="42836-132">In the resulting screen, select the second **Configure account provisioning** button.</span></span>
2. <span data-ttu-id="42836-133">In the **Provisioning Endpoint URL** field, enter the URL of the application's SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-133">In the **Provisioning Endpoint URL** field, enter the URL of the application's SCIM endpoint.</span></span>
3. <span data-ttu-id="42836-134">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the **Authentication Token (optional)** field.</span><span class="sxs-lookup"><span data-stu-id="42836-134">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the **Authentication Token (optional)** field.</span></span> <span data-ttu-id="42836-135">Is this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span><span class="sxs-lookup"><span data-stu-id="42836-135">Is this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="42836-136">Apps that use Azure AD as an idenity provider can validate this Azure AD -issued token.</span><span class="sxs-lookup"><span data-stu-id="42836-136">Apps that use Azure AD as an idenity provider can validate this Azure AD -issued token.</span></span>
4. <span data-ttu-id="42836-137">Click **Next**, and click on the **Start Test** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-137">Click **Next**, and click on the **Start Test** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="42836-138">If the attempts fail, diagnostic information will be displayed.</span><span class="sxs-lookup"><span data-stu-id="42836-138">If the attempts fail, diagnostic information will be displayed.</span></span>  
5. <span data-ttu-id="42836-139">If the attempts to connect to the application succeed, then click **Next** on the remaining screens, and click **Complete** to exit the dialog.</span><span class="sxs-lookup"><span data-stu-id="42836-139">If the attempts to connect to the application succeed, then click **Next** on the remaining screens, and click **Complete** to exit the dialog.</span></span>
6. <span data-ttu-id="42836-140">In the resulting screen, select the third **Assign Accounts** button.</span><span class="sxs-lookup"><span data-stu-id="42836-140">In the resulting screen, select the third **Assign Accounts** button.</span></span> <span data-ttu-id="42836-141">In the resulting Users and Groups section, assign the users or groups you want to provision to the application.</span><span class="sxs-lookup"><span data-stu-id="42836-141">In the resulting Users and Groups section, assign the users or groups you want to provision to the application.</span></span>
7. <span data-ttu-id="42836-142">Once users and groups are assigned, click the **Configure** tab near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="42836-142">Once users and groups are assigned, click the **Configure** tab near the top of the screen.</span></span>
8. <span data-ttu-id="42836-143">Under **Account Provisioning**, confirm that the Status is set to On.</span><span class="sxs-lookup"><span data-stu-id="42836-143">Under **Account Provisioning**, confirm that the Status is set to On.</span></span> 
9. <span data-ttu-id="42836-144">Under **Tools**, click **Restart account provisioning** to kick-start the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="42836-144">Under **Tools**, click **Restart account provisioning** to kick-start the provisioning process.</span></span>

<span data-ttu-id="42836-145">Note that 5-10 minutes may elapse before the provisioning process will begin to send requests to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-145">Note that 5-10 minutes may elapse before the provisioning process will begin to send requests to the SCIM endpoint.</span></span>  <span data-ttu-id="42836-146">A summary of connection attempts is provided on the application’s Dashboard tab, and both a report of provisioning activity and any provisioning errors can be downloaded from the directory’s Reports tab.</span><span class="sxs-lookup"><span data-stu-id="42836-146">A summary of connection attempts is provided on the application’s Dashboard tab, and both a report of provisioning activity and any provisioning errors can be downloaded from the directory’s Reports tab.</span></span>

## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="42836-147">Building Your Own Provisioning Solution For Any Application</span><span class="sxs-lookup"><span data-stu-id="42836-147">Building Your Own Provisioning Solution For Any Application</span></span>
<span data-ttu-id="42836-148">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span><span class="sxs-lookup"><span data-stu-id="42836-148">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="42836-149">Here’s how it works:</span><span class="sxs-lookup"><span data-stu-id="42836-149">Here’s how it works:</span></span>

1. <span data-ttu-id="42836-150">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="42836-150">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="42836-151">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span><span class="sxs-lookup"><span data-stu-id="42836-151">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="42836-152">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span><span class="sxs-lookup"><span data-stu-id="42836-152">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="42836-153">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="42836-153">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="42836-154">Users and groups are assigned to this application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42836-154">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="42836-155">Upon assignment, they are put into a queue to be synchronized to the target application.</span><span class="sxs-lookup"><span data-stu-id="42836-155">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="42836-156">The synchronization process handling the queue runs every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="42836-156">The synchronization process handling the queue runs every 5 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="42836-157">Code Samples</span><span class="sxs-lookup"><span data-stu-id="42836-157">Code Samples</span></span>
<span data-ttu-id="42836-158">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span><span class="sxs-lookup"><span data-stu-id="42836-158">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="42836-159">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span><span class="sxs-lookup"><span data-stu-id="42836-159">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="42836-160">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span><span class="sxs-lookup"><span data-stu-id="42836-160">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="42836-161">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="42836-161">**Prerequisites**</span></span>

* <span data-ttu-id="42836-162">Visual Studio 2013 or later</span><span class="sxs-lookup"><span data-stu-id="42836-162">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="42836-163">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="42836-163">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="42836-164">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-164">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="42836-165">This machine must be accessible from the cloud</span><span class="sxs-lookup"><span data-stu-id="42836-165">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="42836-166">An Azure subscription with a trial or licensed version of Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="42836-166">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="42836-167">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="42836-167">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="42836-168">See the README file included with the sample for additional details</span><span class="sxs-lookup"><span data-stu-id="42836-168">See the README file included with the sample for additional details</span></span>

### <a name="getting-started"></a><span data-ttu-id="42836-169">Getting Started</span><span class="sxs-lookup"><span data-stu-id="42836-169">Getting Started</span></span>
<span data-ttu-id="42836-170">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="42836-170">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="42836-171">**To create a sample SCIM endpoint:**</span><span class="sxs-lookup"><span data-stu-id="42836-171">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="42836-172">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="42836-172">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="42836-173">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="42836-173">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="42836-174">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42836-174">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="42836-175">Select **Tools > Library Package Manager > Package Manager Console**, and execute the commands below for the FileProvisioningAgent project to resolve the solution references:</span><span class="sxs-lookup"><span data-stu-id="42836-175">Select **Tools > Library Package Manager > Package Manager Console**, and execute the commands below for the FileProvisioningAgent project to resolve the solution references:</span></span>
   
   <span data-ttu-id="42836-176">Install-Package Microsoft.SystemForCrossDomainIdentityManagement Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory Install-Package Microsoft.Owin.Diagnostics Install-Package Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="42836-176">Install-Package Microsoft.SystemForCrossDomainIdentityManagement Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory Install-Package Microsoft.Owin.Diagnostics Install-Package Microsoft.Owin.Host.SystemWeb</span></span>
5. <span data-ttu-id="42836-177">Build the FileProvisioningAgent project.</span><span class="sxs-lookup"><span data-stu-id="42836-177">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="42836-178">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="42836-178">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="42836-179">Run the command below, replacing <ip-address> with the IP or domain name of the Windows Machine.</span><span class="sxs-lookup"><span data-stu-id="42836-179">Run the command below, replacing <ip-address> with the IP or domain name of the Windows Machine.</span></span>
   
   <span data-ttu-id="42836-180">FileAgnt.exe http://<ip-address>:9000 TargetFile.csv</span><span class="sxs-lookup"><span data-stu-id="42836-180">FileAgnt.exe http://<ip-address>:9000 TargetFile.csv</span></span>
8. <span data-ttu-id="42836-181">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span><span class="sxs-lookup"><span data-stu-id="42836-181">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="42836-182">If the Windows machine is behind a router, the router will need to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span><span class="sxs-lookup"><span data-stu-id="42836-182">If the Windows machine is behind a router, the router will need to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="42836-183">This is required for Azure AD to be able to access this endpoint in the cloud.</span><span class="sxs-lookup"><span data-stu-id="42836-183">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="42836-184">**To register the sample SCIM endpoint in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="42836-184">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="42836-185">In a web browser, launch the Azure management portal at https://manage.windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="42836-185">In a web browser, launch the Azure management portal at https://manage.windowsazure.com.</span></span>
2. <span data-ttu-id="42836-186">Browse to **Active Directory > Directory > [Your Directory] > Applications**, and select **Add > Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="42836-186">Browse to **Active Directory > Directory > [Your Directory] > Applications**, and select **Add > Add an application from the gallery**.</span></span>
3. <span data-ttu-id="42836-187">Select the **Custom** tab on the left, enter a name such as “SCIM Test App”, and click the checkmark icon to create an app object.</span><span class="sxs-lookup"><span data-stu-id="42836-187">Select the **Custom** tab on the left, enter a name such as “SCIM Test App”, and click the checkmark icon to create an app object.</span></span> <span data-ttu-id="42836-188">Note that the application object created is intend to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-188">Note that the application object created is intend to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>

![][2]

1. <span data-ttu-id="42836-189">In the resulting screen, select the second **Configure account provisioning** button.</span><span class="sxs-lookup"><span data-stu-id="42836-189">In the resulting screen, select the second **Configure account provisioning** button.</span></span>
2. <span data-ttu-id="42836-190">In the dialog, enter the internet-exposed URL and port of your SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-190">In the dialog, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="42836-191">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span><span class="sxs-lookup"><span data-stu-id="42836-191">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
3. <span data-ttu-id="42836-192">Click **Next**, and click on the **Start Test** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-192">Click **Next**, and click on the **Start Test** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="42836-193">If the attempts fail, diagnostic information will be displayed.</span><span class="sxs-lookup"><span data-stu-id="42836-193">If the attempts fail, diagnostic information will be displayed.</span></span>  
4. <span data-ttu-id="42836-194">If the attempts to connect to your Web service succeed, then click **Next** on the remaining screens, and click **Complete** to exit the dialog.</span><span class="sxs-lookup"><span data-stu-id="42836-194">If the attempts to connect to your Web service succeed, then click **Next** on the remaining screens, and click **Complete** to exit the dialog.</span></span>
5. <span data-ttu-id="42836-195">In the resulting screen, select the third **Assign Accounts** button.</span><span class="sxs-lookup"><span data-stu-id="42836-195">In the resulting screen, select the third **Assign Accounts** button.</span></span> <span data-ttu-id="42836-196">In the resulting Users and Groups section, assign the users or groups you want to provision to the application.</span><span class="sxs-lookup"><span data-stu-id="42836-196">In the resulting Users and Groups section, assign the users or groups you want to provision to the application.</span></span>
6. <span data-ttu-id="42836-197">Once users and groups are assigned, click the **Configure** tab near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="42836-197">Once users and groups are assigned, click the **Configure** tab near the top of the screen.</span></span>
7. <span data-ttu-id="42836-198">Under **Account Provisioning**, confirm that the Status is set to On.</span><span class="sxs-lookup"><span data-stu-id="42836-198">Under **Account Provisioning**, confirm that the Status is set to On.</span></span> 
8. <span data-ttu-id="42836-199">Under **Tools**, click **Restart account provisioning** to kick-start the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="42836-199">Under **Tools**, click **Restart account provisioning** to kick-start the provisioning process.</span></span>

<span data-ttu-id="42836-200">Note that 5-10 minutes may elapse before the provisioning process will begin to send requests to the SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="42836-200">Note that 5-10 minutes may elapse before the provisioning process will begin to send requests to the SCIM endpoint.</span></span>  <span data-ttu-id="42836-201">A summary of connection attempts is provided on the application’s Dashboard tab, and both a report of provisioning activity and any provisioning errors can be downloaded from the directory’s Reports tab.</span><span class="sxs-lookup"><span data-stu-id="42836-201">A summary of connection attempts is provided on the application’s Dashboard tab, and both a report of provisioning activity and any provisioning errors can be downloaded from the directory’s Reports tab.</span></span>

<span data-ttu-id="42836-202">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="42836-202">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="42836-203">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span><span class="sxs-lookup"><span data-stu-id="42836-203">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="42836-204">Development Libraries</span><span class="sxs-lookup"><span data-stu-id="42836-204">Development Libraries</span></span>
<span data-ttu-id="42836-205">To develop your own Web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span><span class="sxs-lookup"><span data-stu-id="42836-205">To develop your own Web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

<span data-ttu-id="42836-206">**1:**  Common Language Infrastructure libraries are offered for use with languages based on that infrastructure, such as C#.</span><span class="sxs-lookup"><span data-stu-id="42836-206">**1:**  Common Language Infrastructure libraries are offered for use with languages based on that infrastructure, such as C#.</span></span>  <span data-ttu-id="42836-207">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="42836-207">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the figure below.</span></span>  <span data-ttu-id="42836-208">A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span><span class="sxs-lookup"><span data-stu-id="42836-208">A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span>  <span data-ttu-id="42836-209">The libraries enable the developer to easily deploy a Web service that conforms to the SCIM specification, either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span><span class="sxs-lookup"><span data-stu-id="42836-209">The libraries enable the developer to easily deploy a Web service that conforms to the SCIM specification, either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span>  <span data-ttu-id="42836-210">Requests to that Web service will be translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span><span class="sxs-lookup"><span data-stu-id="42836-210">Requests to that Web service will be translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>    

![][3]

<span data-ttu-id="42836-211">**2:**  [Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js Web service.</span><span class="sxs-lookup"><span data-stu-id="42836-211">**2:**  [Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js Web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="42836-212">Building a Custom SCIM Endpoint</span><span class="sxs-lookup"><span data-stu-id="42836-212">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="42836-213">Using the libraries described above, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="42836-213">Using the libraries described above, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span>  <span data-ttu-id="42836-214">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="42836-214">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="42836-215">It is important to note that this service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span><span class="sxs-lookup"><span data-stu-id="42836-215">It is important to note that this service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="42836-216">CNNIC</span><span class="sxs-lookup"><span data-stu-id="42836-216">CNNIC</span></span>
* <span data-ttu-id="42836-217">Comodo</span><span class="sxs-lookup"><span data-stu-id="42836-217">Comodo</span></span>
* <span data-ttu-id="42836-218">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="42836-218">CyberTrust</span></span>
* <span data-ttu-id="42836-219">DigiCert</span><span class="sxs-lookup"><span data-stu-id="42836-219">DigiCert</span></span>
* <span data-ttu-id="42836-220">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="42836-220">GeoTrust</span></span>
* <span data-ttu-id="42836-221">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="42836-221">GlobalSign</span></span>
* <span data-ttu-id="42836-222">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="42836-222">Go Daddy</span></span>
* <span data-ttu-id="42836-223">Verisign</span><span class="sxs-lookup"><span data-stu-id="42836-223">Verisign</span></span>
* <span data-ttu-id="42836-224">WoSign</span><span class="sxs-lookup"><span data-stu-id="42836-224">WoSign</span></span>

<span data-ttu-id="42836-225">A server authentication certificate can be bound to a port on a Windows host using the network shell utility, like so:</span><span class="sxs-lookup"><span data-stu-id="42836-225">A server authentication certificate can be bound to a port on a Windows host using the network shell utility, like so:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="42836-226">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally-unique identifier.</span><span class="sxs-lookup"><span data-stu-id="42836-226">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally-unique identifier.</span></span>  

<span data-ttu-id="42836-227">To host the service within Internet Information Services, a developer would build a Common Language Infrastructure code library assembly with a class named Startup in the default namespace of the assembly.</span><span class="sxs-lookup"><span data-stu-id="42836-227">To host the service within Internet Information Services, a developer would build a Common Language Infrastructure code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="42836-228">Here is a sample of such a class:</span><span class="sxs-lookup"><span data-stu-id="42836-228">Here is a sample of such a class:</span></span> 

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
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="42836-229">Handling Endpoint Authentication</span><span class="sxs-lookup"><span data-stu-id="42836-229">Handling Endpoint Authentication</span></span>
<span data-ttu-id="42836-230">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span><span class="sxs-lookup"><span data-stu-id="42836-230">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="42836-231">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to Azure Active Directory’s Graph Web service.</span><span class="sxs-lookup"><span data-stu-id="42836-231">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to Azure Active Directory’s Graph Web service.</span></span>  <span data-ttu-id="42836-232">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="42836-232">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="42836-233">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span><span class="sxs-lookup"><span data-stu-id="42836-233">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="42836-234">If the token was issued for accessing the Azure Active Directory’s Graph Web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span><span class="sxs-lookup"><span data-stu-id="42836-234">If the token was issued for accessing the Azure Active Directory’s Graph Web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="42836-235">Developers using the Common Language Infrastructure libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span><span class="sxs-lookup"><span data-stu-id="42836-235">Developers using the Common Language Infrastructure libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

<span data-ttu-id="42836-236">**1:**  In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span><span class="sxs-lookup"><span data-stu-id="42836-236">**1:**  In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

<span data-ttu-id="42836-237">**2:**  Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to Azure Active Directory’s Graph Web service:</span><span class="sxs-lookup"><span data-stu-id="42836-237">**2:**  Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to Azure Active Directory’s Graph Web service:</span></span> 

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

## <a name="user-and-group-schema"></a><span data-ttu-id="42836-238">User and Group Schema</span><span class="sxs-lookup"><span data-stu-id="42836-238">User and Group Schema</span></span>
<span data-ttu-id="42836-239">Azure Active Directory can provision two types of resources to SCIM Web Services.</span><span class="sxs-lookup"><span data-stu-id="42836-239">Azure Active Directory can provision two types of resources to SCIM Web Services.</span></span>  <span data-ttu-id="42836-240">Those types of resources are users and groups.</span><span class="sxs-lookup"><span data-stu-id="42836-240">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="42836-241">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="42836-241">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="42836-242">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span><span class="sxs-lookup"><span data-stu-id="42836-242">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="42836-243">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="42836-243">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="42836-244">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span><span class="sxs-lookup"><span data-stu-id="42836-244">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="42836-245">Table 1: Default user attribute mapping</span><span class="sxs-lookup"><span data-stu-id="42836-245">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="42836-246">Azure Active Directory user</span><span class="sxs-lookup"><span data-stu-id="42836-246">Azure Active Directory user</span></span> | <span data-ttu-id="42836-247">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="42836-247">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="42836-248">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="42836-248">IsSoftDeleted</span></span> |<span data-ttu-id="42836-249">active</span><span class="sxs-lookup"><span data-stu-id="42836-249">active</span></span> |
| <span data-ttu-id="42836-250">displayName</span><span class="sxs-lookup"><span data-stu-id="42836-250">displayName</span></span> |<span data-ttu-id="42836-251">displayName</span><span class="sxs-lookup"><span data-stu-id="42836-251">displayName</span></span> |
| <span data-ttu-id="42836-252">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="42836-252">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="42836-253">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="42836-253">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="42836-254">givenName</span><span class="sxs-lookup"><span data-stu-id="42836-254">givenName</span></span> |<span data-ttu-id="42836-255">name.givenName</span><span class="sxs-lookup"><span data-stu-id="42836-255">name.givenName</span></span> |
| <span data-ttu-id="42836-256">jobTitle</span><span class="sxs-lookup"><span data-stu-id="42836-256">jobTitle</span></span> |<span data-ttu-id="42836-257">title</span><span class="sxs-lookup"><span data-stu-id="42836-257">title</span></span> |
| <span data-ttu-id="42836-258">mail</span><span class="sxs-lookup"><span data-stu-id="42836-258">mail</span></span> |<span data-ttu-id="42836-259">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="42836-259">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="42836-260">mailNickname</span><span class="sxs-lookup"><span data-stu-id="42836-260">mailNickname</span></span> |<span data-ttu-id="42836-261">externalId</span><span class="sxs-lookup"><span data-stu-id="42836-261">externalId</span></span> |
| <span data-ttu-id="42836-262">manager</span><span class="sxs-lookup"><span data-stu-id="42836-262">manager</span></span> |<span data-ttu-id="42836-263">manager</span><span class="sxs-lookup"><span data-stu-id="42836-263">manager</span></span> |
| <span data-ttu-id="42836-264">mobile</span><span class="sxs-lookup"><span data-stu-id="42836-264">mobile</span></span> |<span data-ttu-id="42836-265">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="42836-265">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="42836-266">objectId</span><span class="sxs-lookup"><span data-stu-id="42836-266">objectId</span></span> |<span data-ttu-id="42836-267">id</span><span class="sxs-lookup"><span data-stu-id="42836-267">id</span></span> |
| <span data-ttu-id="42836-268">postalCode</span><span class="sxs-lookup"><span data-stu-id="42836-268">postalCode</span></span> |<span data-ttu-id="42836-269">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="42836-269">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="42836-270">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="42836-270">proxy-Addresses</span></span> |<span data-ttu-id="42836-271">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="42836-271">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="42836-272">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="42836-272">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="42836-273">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="42836-273">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="42836-274">streetAddress</span><span class="sxs-lookup"><span data-stu-id="42836-274">streetAddress</span></span> |<span data-ttu-id="42836-275">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="42836-275">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="42836-276">surname</span><span class="sxs-lookup"><span data-stu-id="42836-276">surname</span></span> |<span data-ttu-id="42836-277">name.familyName</span><span class="sxs-lookup"><span data-stu-id="42836-277">name.familyName</span></span> |
| <span data-ttu-id="42836-278">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="42836-278">telephone-Number</span></span> |<span data-ttu-id="42836-279">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="42836-279">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="42836-280">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="42836-280">user-PrincipalName</span></span> |<span data-ttu-id="42836-281">userName</span><span class="sxs-lookup"><span data-stu-id="42836-281">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="42836-282">Table 2: Default group attribute mapping</span><span class="sxs-lookup"><span data-stu-id="42836-282">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="42836-283">Azure Active Directory group</span><span class="sxs-lookup"><span data-stu-id="42836-283">Azure Active Directory group</span></span> | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| <span data-ttu-id="42836-284">displayName</span><span class="sxs-lookup"><span data-stu-id="42836-284">displayName</span></span> |<span data-ttu-id="42836-285">externalId</span><span class="sxs-lookup"><span data-stu-id="42836-285">externalId</span></span> |
| <span data-ttu-id="42836-286">mail</span><span class="sxs-lookup"><span data-stu-id="42836-286">mail</span></span> |<span data-ttu-id="42836-287">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="42836-287">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="42836-288">mailNickname</span><span class="sxs-lookup"><span data-stu-id="42836-288">mailNickname</span></span> |<span data-ttu-id="42836-289">displayName</span><span class="sxs-lookup"><span data-stu-id="42836-289">displayName</span></span> |
| <span data-ttu-id="42836-290">members</span><span class="sxs-lookup"><span data-stu-id="42836-290">members</span></span> |<span data-ttu-id="42836-291">members</span><span class="sxs-lookup"><span data-stu-id="42836-291">members</span></span> |
| <span data-ttu-id="42836-292">objectId</span><span class="sxs-lookup"><span data-stu-id="42836-292">objectId</span></span> |<span data-ttu-id="42836-293">id</span><span class="sxs-lookup"><span data-stu-id="42836-293">id</span></span> |
| <span data-ttu-id="42836-294">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="42836-294">proxyAddresses</span></span> |<span data-ttu-id="42836-295">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="42836-295">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="42836-296">User Provisioning and De-Provisioning</span><span class="sxs-lookup"><span data-stu-id="42836-296">User Provisioning and De-Provisioning</span></span>
<span data-ttu-id="42836-297">The figure below shows the messages that Azure Active Directory will send to a SCIM service to manage the lifecycle of a user in another identity store.</span><span class="sxs-lookup"><span data-stu-id="42836-297">The figure below shows the messages that Azure Active Directory will send to a SCIM service to manage the lifecycle of a user in another identity store.</span></span>  <span data-ttu-id="42836-298">The diagram also shows how a SCIM service implemented using the Common Language Infrastructure libraries provided by Microsoft for building such services will translate those requests into calls to the methods of a provider.</span><span class="sxs-lookup"><span data-stu-id="42836-298">The diagram also shows how a SCIM service implemented using the Common Language Infrastructure libraries provided by Microsoft for building such services will translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="42836-299">![][4]
*Figure: User provisioning and de-provisioning sequence*</span><span class="sxs-lookup"><span data-stu-id="42836-299">![][4]
*Figure: User provisioning and de-provisioning sequence*</span></span>

<span data-ttu-id="42836-300">**1:**  Azure Active Directory will query the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42836-300">**1:**  Azure Active Directory will query the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure Active Directory.</span></span>  <span data-ttu-id="42836-301">The query will be expressed as a Hypertext Transfer Protocol request like this one, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="42836-301">The query will be expressed as a Hypertext Transfer Protocol request like this one, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 

    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...

<span data-ttu-id="42836-302">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Query method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-302">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="42836-303">Here is the signature of that method:</span><span class="sxs-lookup"><span data-stu-id="42836-303">Here is the signature of that method:</span></span> 

    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);

<span data-ttu-id="42836-304">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span><span class="sxs-lookup"><span data-stu-id="42836-304">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 

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

<span data-ttu-id="42836-305">In the case of the foregoing sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method will be as follows:</span><span class="sxs-lookup"><span data-stu-id="42836-305">In the case of the foregoing sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method will be as follows:</span></span> 

* <span data-ttu-id="42836-306">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="42836-306">parameters.AlternateFilters.Count: 1</span></span>
* <span data-ttu-id="42836-307">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="42836-307">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
* <span data-ttu-id="42836-308">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="42836-308">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
* <span data-ttu-id="42836-309">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="42836-309">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
* <span data-ttu-id="42836-310">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="42836-310">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

<span data-ttu-id="42836-311">**2:**  If the response to a query to the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure Active Directory does not return any users, then Azure Active Directory will request that the service provision a user corresponding to the one in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42836-311">**2:**  If the response to a query to the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure Active Directory does not return any users, then Azure Active Directory will request that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="42836-312">Here is an example of such a request:</span><span class="sxs-lookup"><span data-stu-id="42836-312">Here is an example of such a request:</span></span> 

    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
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

<span data-ttu-id="42836-313">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-313">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="42836-314">The Create method has this signature:</span><span class="sxs-lookup"><span data-stu-id="42836-314">The Create method has this signature:</span></span> 

    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);

<span data-ttu-id="42836-315">In the case of a request to provision a user, the value of the resource argument will be an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="42836-315">In the case of a request to provision a user, the value of the resource argument will be an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="42836-316">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span><span class="sxs-lookup"><span data-stu-id="42836-316">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="42836-317">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the the Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="42836-317">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="42836-318">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly-provisioned user.</span><span class="sxs-lookup"><span data-stu-id="42836-318">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly-provisioned user.</span></span>  

<span data-ttu-id="42836-319">**3:**  To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory will proceed by requesting the current state of that user from the service with a request like this one:</span><span class="sxs-lookup"><span data-stu-id="42836-319">**3:**  To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory will proceed by requesting the current state of that user from the service with a request like this one:</span></span> 

    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...

<span data-ttu-id="42836-320">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request will be translated into a call to the Retrieve method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-320">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request will be translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="42836-321">Here is the signature of the Retrieve method:</span><span class="sxs-lookup"><span data-stu-id="42836-321">Here is the signature of the Retrieve method:</span></span> 

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

<span data-ttu-id="42836-322">In the case of the foregoing example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument will be as follows:</span><span class="sxs-lookup"><span data-stu-id="42836-322">In the case of the foregoing example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument will be as follows:</span></span> 

* <span data-ttu-id="42836-323">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="42836-323">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
* <span data-ttu-id="42836-324">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="42836-324">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

<span data-ttu-id="42836-325">**4:**  If a reference attribute is to be updated, then Azure Active Directory will query the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42836-325">**4:**  If a reference attribute is to be updated, then Azure Active Directory will query the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span>  <span data-ttu-id="42836-326">In the case of users, the only attribute of which the current value will be queried in this way is the manager attribute.</span><span class="sxs-lookup"><span data-stu-id="42836-326">In the case of users, the only attribute of which the current value will be queried in this way is the manager attribute.</span></span>  <span data-ttu-id="42836-327">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span><span class="sxs-lookup"><span data-stu-id="42836-327">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 

    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...

<span data-ttu-id="42836-328">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span><span class="sxs-lookup"><span data-stu-id="42836-328">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="42836-329">Of course, the value of the id attribute is known to the requestor—it is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span><span class="sxs-lookup"><span data-stu-id="42836-329">Of course, the value of the id attribute is known to the requestor—it is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

<span data-ttu-id="42836-330">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Query method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-330">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="42836-331">The value of the properties of the object provided as the value of the parameters argument will be as follows:</span><span class="sxs-lookup"><span data-stu-id="42836-331">The value of the properties of the object provided as the value of the parameters argument will be as follows:</span></span> 

* <span data-ttu-id="42836-332">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="42836-332">parameters.AlternateFilters.Count: 2</span></span>
* <span data-ttu-id="42836-333">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="42836-333">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
* <span data-ttu-id="42836-334">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="42836-334">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
* <span data-ttu-id="42836-335">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="42836-335">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
* <span data-ttu-id="42836-336">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="42836-336">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
* <span data-ttu-id="42836-337">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="42836-337">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
* <span data-ttu-id="42836-338">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="42836-338">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
* <span data-ttu-id="42836-339">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="42836-339">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
* <span data-ttu-id="42836-340">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="42836-340">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

<span data-ttu-id="42836-341">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span><span class="sxs-lookup"><span data-stu-id="42836-341">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

<span data-ttu-id="42836-342">**5:**  Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span><span class="sxs-lookup"><span data-stu-id="42836-342">**5:**  Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 

    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
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

<span data-ttu-id="42836-343">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-343">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span>  <span data-ttu-id="42836-344">Here is the signature of that method:</span><span class="sxs-lookup"><span data-stu-id="42836-344">Here is the signature of that method:</span></span> 

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



<span data-ttu-id="42836-345">In the case of the foregoing example of a request to update a user, the object provided as the value of the patch argument will have these property values:</span><span class="sxs-lookup"><span data-stu-id="42836-345">In the case of the foregoing example of a request to update a user, the object provided as the value of the patch argument will have these property values:</span></span> 

* <span data-ttu-id="42836-346">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="42836-346">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
* <span data-ttu-id="42836-347">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="42836-347">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
* <span data-ttu-id="42836-348">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="42836-348">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
* <span data-ttu-id="42836-349">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="42836-349">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
* <span data-ttu-id="42836-350">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="42836-350">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
* <span data-ttu-id="42836-351">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="42836-351">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
* <span data-ttu-id="42836-352">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="42836-352">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
* <span data-ttu-id="42836-353">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="42836-353">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

<span data-ttu-id="42836-354">**6:**  To de-provision a user from an identity store fronted by an SCIM service, Azure Active Directory will send a request like this one:</span><span class="sxs-lookup"><span data-stu-id="42836-354">**6:**  To de-provision a user from an identity store fronted by an SCIM service, Azure Active Directory will send a request like this one:</span></span> 

    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...

<span data-ttu-id="42836-355">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Delete method of the service’s provider.</span><span class="sxs-lookup"><span data-stu-id="42836-355">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request will be translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="42836-356">That method has this signature:</span><span class="sxs-lookup"><span data-stu-id="42836-356">That method has this signature:</span></span> 

    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);

<span data-ttu-id="42836-357">The object provided as the value of the resourceIdentifier argument will have these property values in the case of the foregoing example of a request to de-provision a user:</span><span class="sxs-lookup"><span data-stu-id="42836-357">The object provided as the value of the resourceIdentifier argument will have these property values in the case of the foregoing example of a request to de-provision a user:</span></span> 

* <span data-ttu-id="42836-358">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="42836-358">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
* <span data-ttu-id="42836-359">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="42836-359">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="42836-360">Group Provisioning and De-Provisioning</span><span class="sxs-lookup"><span data-stu-id="42836-360">Group Provisioning and De-Provisioning</span></span>
<span data-ttu-id="42836-361">The figure below shows the messages that Azure Active Directory will send to a SCIM service to manage the lifecycle of a group in another identity store.</span><span class="sxs-lookup"><span data-stu-id="42836-361">The figure below shows the messages that Azure Active Directory will send to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="42836-362">Those messages differ from the messages pertaining to users in three ways:</span><span class="sxs-lookup"><span data-stu-id="42836-362">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="42836-363">The schema of a group resource will be identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="42836-363">The schema of a group resource will be identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="42836-364">Requests to retrieve groups will stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span><span class="sxs-lookup"><span data-stu-id="42836-364">Requests to retrieve groups will stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="42836-365">Requests to determine whether a reference attribute has a certain value will be requests about the members attribute.</span><span class="sxs-lookup"><span data-stu-id="42836-365">Requests to determine whether a reference attribute has a certain value will be requests about the members attribute.</span></span>  

<span data-ttu-id="42836-366">![][5]
*Figure: Group provisioning and de-provisioning sequence*</span><span class="sxs-lookup"><span data-stu-id="42836-366">![][5]
*Figure: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="42836-367">Related Articles</span><span class="sxs-lookup"><span data-stu-id="42836-367">Related Articles</span></span>
* [<span data-ttu-id="42836-368">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42836-368">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="42836-369">Automate User Provisioning/Deprovisioning to SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="42836-369">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="42836-370">Customizing Attribute Mappings for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="42836-370">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="42836-371">Writing Expressions for Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="42836-371">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="42836-372">Scoping Filters for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="42836-372">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="42836-373">Account Provisioning Notifications</span><span class="sxs-lookup"><span data-stu-id="42836-373">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="42836-374">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="42836-374">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-scim-provisioning/scim-figure-1.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-scim-provisioning/scim-figure-2.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-scim-provisioning/scim-figure-5.PNG





