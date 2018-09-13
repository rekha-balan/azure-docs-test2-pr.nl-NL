---
title: Azure MFA software development kit for custom apps
description: This article shows you how to download and use the Azure MFA SDK to enable two-step verification for your custom apps.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 6b82ba53e7a469b01d77865831c2f5fb37f71044
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865365"
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="0c396-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span><span class="sxs-lookup"><span data-stu-id="0c396-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c396-104">The deprecation of the Azure Multi-Factor Authentication Software Development Kit (SDK) has been announced.</span><span class="sxs-lookup"><span data-stu-id="0c396-104">The deprecation of the Azure Multi-Factor Authentication Software Development Kit (SDK) has been announced.</span></span> <span data-ttu-id="0c396-105">This feature will no longer be supported for new customers.</span><span class="sxs-lookup"><span data-stu-id="0c396-105">This feature will no longer be supported for new customers.</span></span> <span data-ttu-id="0c396-106">Current customers can continue using the SDK until November 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="0c396-106">Current customers can continue using the SDK until November 14, 2018.</span></span> <span data-ttu-id="0c396-107">After that time, calls to the SDK will fail.</span><span class="sxs-lookup"><span data-stu-id="0c396-107">After that time, calls to the SDK will fail.</span></span> 

<span data-ttu-id="0c396-108">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="0c396-108">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="0c396-109">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="0c396-109">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="0c396-110">The SDK provides a thin wrapper around two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0c396-110">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="0c396-111">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span><span class="sxs-lookup"><span data-stu-id="0c396-111">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="0c396-112">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span><span class="sxs-lookup"><span data-stu-id="0c396-112">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="0c396-113">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span><span class="sxs-lookup"><span data-stu-id="0c396-113">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="0c396-114">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span><span class="sxs-lookup"><span data-stu-id="0c396-114">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="0c396-115">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span><span class="sxs-lookup"><span data-stu-id="0c396-115">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="0c396-116">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span><span class="sxs-lookup"><span data-stu-id="0c396-116">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="0c396-117">All calls must include a reference to the private certificate that is included in every SDK.</span><span class="sxs-lookup"><span data-stu-id="0c396-117">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="0c396-118">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span><span class="sxs-lookup"><span data-stu-id="0c396-118">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="0c396-119">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span><span class="sxs-lookup"><span data-stu-id="0c396-119">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c396-120">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span><span class="sxs-lookup"><span data-stu-id="0c396-120">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="0c396-121">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span><span class="sxs-lookup"><span data-stu-id="0c396-121">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="0c396-122">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span><span class="sxs-lookup"><span data-stu-id="0c396-122">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="0c396-123">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span><span class="sxs-lookup"><span data-stu-id="0c396-123">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="0c396-124">Download the SDK</span><span class="sxs-lookup"><span data-stu-id="0c396-124">Download the SDK</span></span>
<span data-ttu-id="0c396-125">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](concept-mfa-authprovider.md).</span><span class="sxs-lookup"><span data-stu-id="0c396-125">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](concept-mfa-authprovider.md).</span></span>  <span data-ttu-id="0c396-126">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span><span class="sxs-lookup"><span data-stu-id="0c396-126">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span> <span data-ttu-id="0c396-127">The public methods of downloading the SDK have been decommissioned since the SDK has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="0c396-127">The public methods of downloading the SDK have been decommissioned since the SDK has been deprecated.</span></span> <span data-ttu-id="0c396-128">You should open a support case with Microsoft if you need to download the SDK.</span><span class="sxs-lookup"><span data-stu-id="0c396-128">You should open a support case with Microsoft if you need to download the SDK.</span></span> <span data-ttu-id="0c396-129">The SDK is provided only to customers that are already using the SDK.</span><span class="sxs-lookup"><span data-stu-id="0c396-129">The SDK is provided only to customers that are already using the SDK.</span></span> <span data-ttu-id="0c396-130">New customers will not be onboarded.</span><span class="sxs-lookup"><span data-stu-id="0c396-130">New customers will not be onboarded.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="0c396-131">What's in the SDK</span><span class="sxs-lookup"><span data-stu-id="0c396-131">What's in the SDK</span></span>
<span data-ttu-id="0c396-132">The SDK includes the following items:</span><span class="sxs-lookup"><span data-stu-id="0c396-132">The SDK includes the following items:</span></span>

* <span data-ttu-id="0c396-133">**README**.</span><span class="sxs-lookup"><span data-stu-id="0c396-133">**README**.</span></span> <span data-ttu-id="0c396-134">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span><span class="sxs-lookup"><span data-stu-id="0c396-134">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="0c396-135">**Source files** for Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0c396-135">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="0c396-136">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span><span class="sxs-lookup"><span data-stu-id="0c396-136">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="0c396-137">**Private key** for the certificate</span><span class="sxs-lookup"><span data-stu-id="0c396-137">**Private key** for the certificate</span></span>
* <span data-ttu-id="0c396-138">**Call results.**</span><span class="sxs-lookup"><span data-stu-id="0c396-138">**Call results.**</span></span> <span data-ttu-id="0c396-139">A list of call result codes.</span><span class="sxs-lookup"><span data-stu-id="0c396-139">A list of call result codes.</span></span> <span data-ttu-id="0c396-140">To open this file, use an application with text formatting, such as WordPad.</span><span class="sxs-lookup"><span data-stu-id="0c396-140">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="0c396-141">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span><span class="sxs-lookup"><span data-stu-id="0c396-141">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="0c396-142">They are not authentication status codes.</span><span class="sxs-lookup"><span data-stu-id="0c396-142">They are not authentication status codes.</span></span>
* <span data-ttu-id="0c396-143">**Examples.**</span><span class="sxs-lookup"><span data-stu-id="0c396-143">**Examples.**</span></span> <span data-ttu-id="0c396-144">Sample code for a basic working implementation of Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="0c396-144">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="0c396-145">The client certificate is a unique private certificate that was generated especially for you.</span><span class="sxs-lookup"><span data-stu-id="0c396-145">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="0c396-146">Do not share or lose this file.</span><span class="sxs-lookup"><span data-stu-id="0c396-146">Do not share or lose this file.</span></span> <span data-ttu-id="0c396-147">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span><span class="sxs-lookup"><span data-stu-id="0c396-147">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="0c396-148">Code sample</span><span class="sxs-lookup"><span data-stu-id="0c396-148">Code sample</span></span>
<span data-ttu-id="0c396-149">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span><span class="sxs-lookup"><span data-stu-id="0c396-149">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="0c396-150">Standard mode is a telephone call that the user responds to by pressing the # key.</span><span class="sxs-lookup"><span data-stu-id="0c396-150">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="0c396-151">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span><span class="sxs-lookup"><span data-stu-id="0c396-151">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="0c396-152">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span><span class="sxs-lookup"><span data-stu-id="0c396-152">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0c396-153">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span><span class="sxs-lookup"><span data-stu-id="0c396-153">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="0c396-154">These methods are not designed as primary authentication methods.</span><span class="sxs-lookup"><span data-stu-id="0c396-154">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="0c396-155">Code Sample Overview</span><span class="sxs-lookup"><span data-stu-id="0c396-155">Code Sample Overview</span></span>
<span data-ttu-id="0c396-156">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span><span class="sxs-lookup"><span data-stu-id="0c396-156">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="0c396-157">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span><span class="sxs-lookup"><span data-stu-id="0c396-157">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="0c396-158">The client-side code does not include any Multi-Factor Authentication-specific elements.</span><span class="sxs-lookup"><span data-stu-id="0c396-158">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="0c396-159">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span><span class="sxs-lookup"><span data-stu-id="0c396-159">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="0c396-160">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span><span class="sxs-lookup"><span data-stu-id="0c396-160">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="0c396-161">The server-side code adds standard-mode authentication in Step 2.</span><span class="sxs-lookup"><span data-stu-id="0c396-161">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="0c396-162">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span><span class="sxs-lookup"><span data-stu-id="0c396-162">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="0c396-163">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span><span class="sxs-lookup"><span data-stu-id="0c396-163">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="0c396-164">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span><span class="sxs-lookup"><span data-stu-id="0c396-164">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="0c396-165">The return value indicates the success or failure of the authentication.</span><span class="sxs-lookup"><span data-stu-id="0c396-165">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="0c396-166">The out parameters, callStatus, and errorID, contain additional call result information.</span><span class="sxs-lookup"><span data-stu-id="0c396-166">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="0c396-167">The call result codes are documented in the call results file in the SDK.</span><span class="sxs-lookup"><span data-stu-id="0c396-167">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="0c396-168">This minimal implementation can be written in a few lines.</span><span class="sxs-lookup"><span data-stu-id="0c396-168">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="0c396-169">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span><span class="sxs-lookup"><span data-stu-id="0c396-169">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="0c396-170">Web Client Code</span><span class="sxs-lookup"><span data-stu-id="0c396-170">Web Client Code</span></span>
<span data-ttu-id="0c396-171">The following is web client code for a demo page.</span><span class="sxs-lookup"><span data-stu-id="0c396-171">The following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="0c396-172">Server-Side Code</span><span class="sxs-lookup"><span data-stu-id="0c396-172">Server-Side Code</span></span>
<span data-ttu-id="0c396-173">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span><span class="sxs-lookup"><span data-stu-id="0c396-173">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="0c396-174">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span><span class="sxs-lookup"><span data-stu-id="0c396-174">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

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
