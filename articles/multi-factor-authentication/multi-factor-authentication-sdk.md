---
title: MFA software development kit for custom apps | Microsoft Docs
description: This article shows you how to download and use the Azure MFA SDK to enable two-step verification for your custom apps.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: 09eaabdf14d6b1fdd5b62770d4673198e6998dd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553689"
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="251d5-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span><span class="sxs-lookup"><span data-stu-id="251d5-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="251d5-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="251d5-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="251d5-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="251d5-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="251d5-106">The SDK provides a thin wrapper around two-step verification.</span><span class="sxs-lookup"><span data-stu-id="251d5-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="251d5-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span><span class="sxs-lookup"><span data-stu-id="251d5-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="251d5-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span><span class="sxs-lookup"><span data-stu-id="251d5-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="251d5-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span><span class="sxs-lookup"><span data-stu-id="251d5-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="251d5-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span><span class="sxs-lookup"><span data-stu-id="251d5-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="251d5-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span><span class="sxs-lookup"><span data-stu-id="251d5-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="251d5-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span><span class="sxs-lookup"><span data-stu-id="251d5-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="251d5-113">All calls must include a reference to the private certificate that is included in every SDK.</span><span class="sxs-lookup"><span data-stu-id="251d5-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="251d5-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span><span class="sxs-lookup"><span data-stu-id="251d5-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="251d5-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span><span class="sxs-lookup"><span data-stu-id="251d5-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="251d5-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span><span class="sxs-lookup"><span data-stu-id="251d5-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="251d5-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span><span class="sxs-lookup"><span data-stu-id="251d5-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="251d5-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span><span class="sxs-lookup"><span data-stu-id="251d5-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="251d5-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span><span class="sxs-lookup"><span data-stu-id="251d5-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-azure-multi-factor-authentication-sdk"></a><span data-ttu-id="251d5-120">Download the Azure Multi-Factor Authentication SDK</span><span class="sxs-lookup"><span data-stu-id="251d5-120">Download the Azure Multi-Factor Authentication SDK</span></span>
<span data-ttu-id="251d5-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="251d5-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="251d5-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span><span class="sxs-lookup"><span data-stu-id="251d5-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="251d5-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span><span class="sxs-lookup"><span data-stu-id="251d5-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="251d5-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span><span class="sxs-lookup"><span data-stu-id="251d5-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="to-download-the-azure-multi-factor-authentication-sdk-from-the-azure-classic-portal"></a><span data-ttu-id="251d5-125">To download the Azure Multi-Factor Authentication SDK from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="251d5-125">To download the Azure Multi-Factor Authentication SDK from the Azure classic portal</span></span>
1. <span data-ttu-id="251d5-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="251d5-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="251d5-127">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="251d5-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="251d5-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span><span class="sxs-lookup"><span data-stu-id="251d5-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="251d5-129">At the bottom select **Manage**.</span><span class="sxs-lookup"><span data-stu-id="251d5-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="251d5-130">A new page opens.</span><span class="sxs-lookup"><span data-stu-id="251d5-130">A new page opens.</span></span>
5. <span data-ttu-id="251d5-131">On the left, at the bottom, click **SDK**.</span><span class="sxs-lookup"><span data-stu-id="251d5-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="251d5-132"><center>![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="251d5-132"><center>![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="251d5-133">Select the language you want and click one the associated download links.</span><span class="sxs-lookup"><span data-stu-id="251d5-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="251d5-134">Save the download.</span><span class="sxs-lookup"><span data-stu-id="251d5-134">Save the download.</span></span>

### <a name="to-download-the-azure-multi-factor-authentication-sdk-via-the-service-settings"></a><span data-ttu-id="251d5-135">To download the Azure Multi-Factor Authentication SDK via the service settings</span><span class="sxs-lookup"><span data-stu-id="251d5-135">To download the Azure Multi-Factor Authentication SDK via the service settings</span></span>
1. <span data-ttu-id="251d5-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="251d5-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="251d5-137">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="251d5-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="251d5-138">Double-click your instance of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="251d5-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="251d5-139">At the top click **Configure**</span><span class="sxs-lookup"><span data-stu-id="251d5-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="251d5-140">Under multi-factor authentication, select **Manage service settings**
   ![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="251d5-140">Under multi-factor authentication, select **Manage service settings**
![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="251d5-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span><span class="sxs-lookup"><span data-stu-id="251d5-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="251d5-142">A new page opens.</span><span class="sxs-lookup"><span data-stu-id="251d5-142">A new page opens.</span></span>
   <span data-ttu-id="251d5-143">![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="251d5-143">![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="251d5-144">On the left, at the bottom, click **SDK**.</span><span class="sxs-lookup"><span data-stu-id="251d5-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="251d5-145">Select the language you want and click one the associated download links.</span><span class="sxs-lookup"><span data-stu-id="251d5-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="251d5-146">Save the download.</span><span class="sxs-lookup"><span data-stu-id="251d5-146">Save the download.</span></span>

## <a name="contents-of-the-azure-multi-factor-authentication-sdk"></a><span data-ttu-id="251d5-147">Contents of the Azure Multi-Factor Authentication SDK</span><span class="sxs-lookup"><span data-stu-id="251d5-147">Contents of the Azure Multi-Factor Authentication SDK</span></span>
<span data-ttu-id="251d5-148">Inside the SDK are the following items:</span><span class="sxs-lookup"><span data-stu-id="251d5-148">Inside the SDK are the following items:</span></span>

* <span data-ttu-id="251d5-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="251d5-149">**README**.</span></span> <span data-ttu-id="251d5-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span><span class="sxs-lookup"><span data-stu-id="251d5-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="251d5-151">**Source file(s)** for Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="251d5-151">**Source file(s)** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="251d5-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span><span class="sxs-lookup"><span data-stu-id="251d5-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="251d5-153">**Private key** for the certificate</span><span class="sxs-lookup"><span data-stu-id="251d5-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="251d5-154">**Call results.**</span><span class="sxs-lookup"><span data-stu-id="251d5-154">**Call results.**</span></span> <span data-ttu-id="251d5-155">A list of call result codes.</span><span class="sxs-lookup"><span data-stu-id="251d5-155">A list of call result codes.</span></span> <span data-ttu-id="251d5-156">To open this file, use an application with text formatting, such as WordPad.</span><span class="sxs-lookup"><span data-stu-id="251d5-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="251d5-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span><span class="sxs-lookup"><span data-stu-id="251d5-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="251d5-158">They are not authentication status codes.</span><span class="sxs-lookup"><span data-stu-id="251d5-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="251d5-159">**Examples.**</span><span class="sxs-lookup"><span data-stu-id="251d5-159">**Examples.**</span></span> <span data-ttu-id="251d5-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="251d5-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="251d5-161">The client certificate is a unique private certificate that was generated especially for you.</span><span class="sxs-lookup"><span data-stu-id="251d5-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="251d5-162">Do not share or lose this file.</span><span class="sxs-lookup"><span data-stu-id="251d5-162">Do not share or lose this file.</span></span> <span data-ttu-id="251d5-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span><span class="sxs-lookup"><span data-stu-id="251d5-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample-standard-mode-phone-verification"></a><span data-ttu-id="251d5-164">Code Sample: Standard Mode Phone Verification</span><span class="sxs-lookup"><span data-stu-id="251d5-164">Code Sample: Standard Mode Phone Verification</span></span>
<span data-ttu-id="251d5-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span><span class="sxs-lookup"><span data-stu-id="251d5-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="251d5-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span><span class="sxs-lookup"><span data-stu-id="251d5-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="251d5-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span><span class="sxs-lookup"><span data-stu-id="251d5-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="251d5-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span><span class="sxs-lookup"><span data-stu-id="251d5-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="251d5-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span><span class="sxs-lookup"><span data-stu-id="251d5-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="251d5-170">These methods are not designed as primary authentication methods.</span><span class="sxs-lookup"><span data-stu-id="251d5-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="251d5-171">Code Sample Overview</span><span class="sxs-lookup"><span data-stu-id="251d5-171">Code Sample Overview</span></span>
<span data-ttu-id="251d5-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span><span class="sxs-lookup"><span data-stu-id="251d5-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="251d5-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span><span class="sxs-lookup"><span data-stu-id="251d5-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="251d5-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span><span class="sxs-lookup"><span data-stu-id="251d5-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="251d5-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span><span class="sxs-lookup"><span data-stu-id="251d5-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="251d5-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span><span class="sxs-lookup"><span data-stu-id="251d5-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="251d5-177">The server-side code adds standard-mode authentication in Step 2.</span><span class="sxs-lookup"><span data-stu-id="251d5-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="251d5-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span><span class="sxs-lookup"><span data-stu-id="251d5-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="251d5-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span><span class="sxs-lookup"><span data-stu-id="251d5-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="251d5-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span><span class="sxs-lookup"><span data-stu-id="251d5-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="251d5-181">The return value indicates the success or failure of the authentication.</span><span class="sxs-lookup"><span data-stu-id="251d5-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="251d5-182">The out parameters, callStatus and errorID, contain additional call result information.</span><span class="sxs-lookup"><span data-stu-id="251d5-182">The out parameters, callStatus and errorID, contain additional call result information.</span></span> <span data-ttu-id="251d5-183">The call result codes are documented in the call results file in the SDK.</span><span class="sxs-lookup"><span data-stu-id="251d5-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="251d5-184">This minimal implementation can be written in a few lines.</span><span class="sxs-lookup"><span data-stu-id="251d5-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="251d5-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span><span class="sxs-lookup"><span data-stu-id="251d5-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="251d5-186">Web Client Code</span><span class="sxs-lookup"><span data-stu-id="251d5-186">Web Client Code</span></span>
<span data-ttu-id="251d5-187">The following is web client code for a demo page.</span><span class="sxs-lookup"><span data-stu-id="251d5-187">The following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="251d5-188">Server-Side Code</span><span class="sxs-lookup"><span data-stu-id="251d5-188">Server-Side Code</span></span>
<span data-ttu-id="251d5-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span><span class="sxs-lookup"><span data-stu-id="251d5-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="251d5-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span><span class="sxs-lookup"><span data-stu-id="251d5-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }



