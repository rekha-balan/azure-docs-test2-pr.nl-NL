---
title: 'Azure Active Directory B2C: Use the Graph API | Microsoft Docs'
description: How to call the Graph API for a B2C tenant by using an application identity to automate the process.
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: bryanla
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: a932b617d57184ef714bf18f1e1e23599db52487
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662257"
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="d6dae-103">Azure AD B2C: Use the Graph API</span><span class="sxs-lookup"><span data-stu-id="d6dae-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="d6dae-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span><span class="sxs-lookup"><span data-stu-id="d6dae-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="d6dae-105">This means that many common tenant management tasks need to be performed programmatically.</span><span class="sxs-lookup"><span data-stu-id="d6dae-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="d6dae-106">A primary example is user management.</span><span class="sxs-lookup"><span data-stu-id="d6dae-106">A primary example is user management.</span></span> <span data-ttu-id="d6dae-107">You might need to migrate an existing user store to a B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="d6dae-108">You may want to host user registration on your own page and create user accounts in Azure AD behind the scenes.</span><span class="sxs-lookup"><span data-stu-id="d6dae-108">You may want to host user registration on your own page and create user accounts in Azure AD behind the scenes.</span></span> <span data-ttu-id="d6dae-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span><span class="sxs-lookup"><span data-stu-id="d6dae-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="d6dae-110">You can do these tasks by using the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="d6dae-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="d6dae-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span><span class="sxs-lookup"><span data-stu-id="d6dae-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="d6dae-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="d6dae-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span><span class="sxs-lookup"><span data-stu-id="d6dae-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="d6dae-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6dae-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="d6dae-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d6dae-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="d6dae-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="d6dae-118">In this article, we'll discuss how to perform the automated-use case.</span><span class="sxs-lookup"><span data-stu-id="d6dae-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="d6dae-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span><span class="sxs-lookup"><span data-stu-id="d6dae-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="d6dae-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span><span class="sxs-lookup"><span data-stu-id="d6dae-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="d6dae-121">However, the code is written to behave in a noninteractive, automated fashion.</span><span class="sxs-lookup"><span data-stu-id="d6dae-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d6dae-122">Get an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="d6dae-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="d6dae-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="d6dae-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6dae-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-a-service-application-in-your-tenant"></a><span data-ttu-id="d6dae-125">Register a service application in your tenant</span><span class="sxs-lookup"><span data-stu-id="d6dae-125">Register a service application in your tenant</span></span>
<span data-ttu-id="d6dae-126">After you have a B2C tenant, you need to create your service application by using Azure AD PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d6dae-126">After you have a B2C tenant, you need to create your service application by using Azure AD PowerShell cmdlets.</span></span>
<span data-ttu-id="d6dae-127">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="d6dae-127">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="d6dae-128">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="d6dae-128">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6dae-129">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6dae-129">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using PowerShell.</span></span> <span data-ttu-id="d6dae-130">Follow the instruction in this article to do that.</span><span class="sxs-lookup"><span data-stu-id="d6dae-130">Follow the instruction in this article to do that.</span></span> <span data-ttu-id="d6dae-131">You can't reuse the already-existing B2C applications that you registered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d6dae-131">You can't reuse the already-existing B2C applications that you registered in the Azure portal.</span></span>
> 
> 

<span data-ttu-id="d6dae-132">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-132">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="d6dae-133">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span><span class="sxs-lookup"><span data-stu-id="d6dae-133">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

```
> $msolcred = Get-Credential
> Connect-MsolService -credential $msolcred
```

<span data-ttu-id="d6dae-134">Before you create your application, you need to generate a new **client secret**.</span><span class="sxs-lookup"><span data-stu-id="d6dae-134">Before you create your application, you need to generate a new **client secret**.</span></span>  <span data-ttu-id="d6dae-135">Your application will use the client secret to authenticate to Azure AD and to acquire access tokens.</span><span class="sxs-lookup"><span data-stu-id="d6dae-135">Your application will use the client secret to authenticate to Azure AD and to acquire access tokens.</span></span> <span data-ttu-id="d6dae-136">You can generate a valid secret in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d6dae-136">You can generate a valid secret in PowerShell:</span></span>

```
> $bytes = New-Object Byte[] 32
> $rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
> $rand.GetBytes($bytes)
> $rand.Dispose()
> $newClientSecret = [System.Convert]::ToBase64String($bytes)
> $newClientSecret
```

<span data-ttu-id="d6dae-137">The final command should print your new client secret.</span><span class="sxs-lookup"><span data-stu-id="d6dae-137">The final command should print your new client secret.</span></span> <span data-ttu-id="d6dae-138">Copy it somewhere safe.</span><span class="sxs-lookup"><span data-stu-id="d6dae-138">Copy it somewhere safe.</span></span> <span data-ttu-id="d6dae-139">You'll need it later.</span><span class="sxs-lookup"><span data-stu-id="d6dae-139">You'll need it later.</span></span> <span data-ttu-id="d6dae-140">Now you can create your application by providing the new client secret as a credential for the app:</span><span class="sxs-lookup"><span data-stu-id="d6dae-140">Now you can create your application by providing the new client secret as a credential for the app:</span></span>

```
> New-MsolServicePrincipal -DisplayName "My New B2C Graph API App" -Type password -Value $newClientSecret

DisplayName           : My New B2C Graph API App
ServicePrincipalNames : {dd02c40f-1325-46c2-a118-4659db8a55d5}
ObjectId              : e2bde258-6691-410b-879c-b1f88d9ef664
AppPrincipalId        : dd02c40f-1325-46c2-a118-4659db8a55d5
TrustedForDelegation  : False
AccountEnabled        : True
Addresses             : {}
KeyType               : Password
KeyId                 : a261e39d-953e-4d6a-8d70-1f915e054ef9
StartDate             : 9/2/2015 1:33:09 AM
EndDate               : 9/2/2016 1:33:09 AM
Usage                 : Verify
```

<span data-ttu-id="d6dae-141">If you successfully create the application, it should print out properties of the application like the ones above.</span><span class="sxs-lookup"><span data-stu-id="d6dae-141">If you successfully create the application, it should print out properties of the application like the ones above.</span></span> <span data-ttu-id="d6dae-142">You'll need both `ObjectId` and `AppPrincipalId`, so copy those values, too.</span><span class="sxs-lookup"><span data-stu-id="d6dae-142">You'll need both `ObjectId` and `AppPrincipalId`, so copy those values, too.</span></span>

<span data-ttu-id="d6dae-143">After you create an application in your B2C tenant, you need to assign it the permissions it needs to perform user CRUD operations.</span><span class="sxs-lookup"><span data-stu-id="d6dae-143">After you create an application in your B2C tenant, you need to assign it the permissions it needs to perform user CRUD operations.</span></span> <span data-ttu-id="d6dae-144">Assign the application three roles: directory readers (to read users), directory writers (to create and update users), and a user account administrator (to delete users).</span><span class="sxs-lookup"><span data-stu-id="d6dae-144">Assign the application three roles: directory readers (to read users), directory writers (to create and update users), and a user account administrator (to delete users).</span></span> <span data-ttu-id="d6dae-145">These roles have well-known identifiers, so you can replace the `-RoleMemberObjectId` parameter with `ObjectId` from above and run the following commands.</span><span class="sxs-lookup"><span data-stu-id="d6dae-145">These roles have well-known identifiers, so you can replace the `-RoleMemberObjectId` parameter with `ObjectId` from above and run the following commands.</span></span> <span data-ttu-id="d6dae-146">To see the list of all directory roles, try running `Get-MsolRole`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-146">To see the list of all directory roles, try running `Get-MsolRole`.</span></span>

```
> Add-MsolRoleMember -RoleObjectId 88d8e3e3-8f55-4a1e-953a-9b9898b8876b -RoleMemberObjectId <Your-ObjectId> -RoleMemberType servicePrincipal
> Add-MsolRoleMember -RoleObjectId 9360feb5-f418-4baa-8175-e2a00bac4301 -RoleMemberObjectId <Your-ObjectId> -RoleMemberType servicePrincipal
> Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId <Your-ObjectId> -RoleMemberType servicePrincipal
```

<span data-ttu-id="d6dae-147">You now have an application that has permission to create, read, update, and delete users from your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-147">You now have an application that has permission to create, read, update, and delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="d6dae-148">Download, configure, and build the sample code</span><span class="sxs-lookup"><span data-stu-id="d6dae-148">Download, configure, and build the sample code</span></span>
<span data-ttu-id="d6dae-149">First, download the sample code and get it running.</span><span class="sxs-lookup"><span data-stu-id="d6dae-149">First, download the sample code and get it running.</span></span> <span data-ttu-id="d6dae-150">Then we will take a closer look at it.</span><span class="sxs-lookup"><span data-stu-id="d6dae-150">Then we will take a closer look at it.</span></span>  <span data-ttu-id="d6dae-151">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="d6dae-151">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="d6dae-152">You can also clone it into a directory of your choice:</span><span class="sxs-lookup"><span data-stu-id="d6dae-152">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="d6dae-153">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6dae-153">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="d6dae-154">In the `B2CGraphClient` project, open the file `App.config`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-154">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="d6dae-155">Replace the three app settings with your own values:</span><span class="sxs-lookup"><span data-stu-id="d6dae-155">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="contosob2c.onmicrosoft.com" />
    <add key="b2c:ClientId" value="{The AppPrincipalId from above}" />
    <add key="b2c:ClientSecret" value="{The client secret you generated above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="d6dae-156">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span><span class="sxs-lookup"><span data-stu-id="d6dae-156">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="d6dae-157">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-157">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="d6dae-158">Build user CRUD operations by using the Graph API</span><span class="sxs-lookup"><span data-stu-id="d6dae-158">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="d6dae-159">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span><span class="sxs-lookup"><span data-stu-id="d6dae-159">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="d6dae-160">Then run the `B2C Help` command.</span><span class="sxs-lookup"><span data-stu-id="d6dae-160">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="d6dae-161">This will display a brief description of each command.</span><span class="sxs-lookup"><span data-stu-id="d6dae-161">This will display a brief description of each command.</span></span> <span data-ttu-id="d6dae-162">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-162">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="d6dae-163">Get an access token</span><span class="sxs-lookup"><span data-stu-id="d6dae-163">Get an access token</span></span>
<span data-ttu-id="d6dae-164">Any request to the Graph API requires an access token for authentication.</span><span class="sxs-lookup"><span data-stu-id="d6dae-164">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="d6dae-165">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span><span class="sxs-lookup"><span data-stu-id="d6dae-165">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="d6dae-166">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span><span class="sxs-lookup"><span data-stu-id="d6dae-166">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="d6dae-167">You don't have to use ADAL to get tokens, though.</span><span class="sxs-lookup"><span data-stu-id="d6dae-167">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="d6dae-168">You can also get tokens by crafting HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="d6dae-168">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="d6dae-169">This code sample uses ADAL v2 in order to communicate with the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-169">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="d6dae-170">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-170">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="d6dae-171">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span><span class="sxs-lookup"><span data-stu-id="d6dae-171">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="d6dae-172">The constructor for this class sets up an ADAL authentication scaffolding:</span><span class="sxs-lookup"><span data-stu-id="d6dae-172">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="d6dae-173">We'll use the `B2C Get-User` command as an example.</span><span class="sxs-lookup"><span data-stu-id="d6dae-173">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="d6dae-174">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span><span class="sxs-lookup"><span data-stu-id="d6dae-174">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="d6dae-175">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-175">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="d6dae-176">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span><span class="sxs-lookup"><span data-stu-id="d6dae-176">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="d6dae-177">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span><span class="sxs-lookup"><span data-stu-id="d6dae-177">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="d6dae-178">ADAL then returns an `access_token` that represents the application's identity.</span><span class="sxs-lookup"><span data-stu-id="d6dae-178">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="d6dae-179">Read users</span><span class="sxs-lookup"><span data-stu-id="d6dae-179">Read users</span></span>
<span data-ttu-id="d6dae-180">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span><span class="sxs-lookup"><span data-stu-id="d6dae-180">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="d6dae-181">A request for all of the users in a tenant looks like this:</span><span class="sxs-lookup"><span data-stu-id="d6dae-181">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d6dae-182">To see this request, run:</span><span class="sxs-lookup"><span data-stu-id="d6dae-182">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="d6dae-183">There are two important things to note:</span><span class="sxs-lookup"><span data-stu-id="d6dae-183">There are two important things to note:</span></span>

* <span data-ttu-id="d6dae-184">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span><span class="sxs-lookup"><span data-stu-id="d6dae-184">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="d6dae-185">For B2C tenants, you must use the query parameter `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-185">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="d6dae-186">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span><span class="sxs-lookup"><span data-stu-id="d6dae-186">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="d6dae-187">Create consumer user accounts</span><span class="sxs-lookup"><span data-stu-id="d6dae-187">Create consumer user accounts</span></span>
<span data-ttu-id="d6dae-188">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span><span class="sxs-lookup"><span data-stu-id="d6dae-188">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="d6dae-189">Most of these properties in this request are required to create consumer users.</span><span class="sxs-lookup"><span data-stu-id="d6dae-189">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="d6dae-190">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="d6dae-190">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="d6dae-191">Note that the `//` comments have been included for illustration.</span><span class="sxs-lookup"><span data-stu-id="d6dae-191">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="d6dae-192">Do not include them in an actual request.</span><span class="sxs-lookup"><span data-stu-id="d6dae-192">Do not include them in an actual request.</span></span>

<span data-ttu-id="d6dae-193">To see the request, run one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="d6dae-193">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d6dae-194">The `Create-User` command takes a .json file as an input parameter.</span><span class="sxs-lookup"><span data-stu-id="d6dae-194">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="d6dae-195">This contains a JSON representation of a user object.</span><span class="sxs-lookup"><span data-stu-id="d6dae-195">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="d6dae-196">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-196">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="d6dae-197">You can modify these files to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="d6dae-197">You can modify these files to suit your needs.</span></span> <span data-ttu-id="d6dae-198">In addition to the required fields above, several optional fields that you can use are included in these files.</span><span class="sxs-lookup"><span data-stu-id="d6dae-198">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="d6dae-199">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="d6dae-199">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="d6dae-200">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-200">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="d6dae-201">It attaches an access token to the `Authorization` header of the request.</span><span class="sxs-lookup"><span data-stu-id="d6dae-201">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="d6dae-202">It sets `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-202">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="d6dae-203">It includes the JSON user object in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="d6dae-203">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="d6dae-204">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span><span class="sxs-lookup"><span data-stu-id="d6dae-204">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="d6dae-205">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-205">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="d6dae-206">Update consumer user accounts</span><span class="sxs-lookup"><span data-stu-id="d6dae-206">Update consumer user accounts</span></span>
<span data-ttu-id="d6dae-207">When you update user objects, the process is similar to the one you use to create user objects.</span><span class="sxs-lookup"><span data-stu-id="d6dae-207">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="d6dae-208">But this process uses the HTTP `PATCH` method:</span><span class="sxs-lookup"><span data-stu-id="d6dae-208">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="d6dae-209">Try to update a user by updating your JSON files with new data.</span><span class="sxs-lookup"><span data-stu-id="d6dae-209">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="d6dae-210">You can then use `B2CGraphClient` to run one of these commands:</span><span class="sxs-lookup"><span data-stu-id="d6dae-210">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d6dae-211">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span><span class="sxs-lookup"><span data-stu-id="d6dae-211">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="d6dae-212">Search users</span><span class="sxs-lookup"><span data-stu-id="d6dae-212">Search users</span></span>
<span data-ttu-id="d6dae-213">You can search for users in your B2C tenant in a couple of ways.</span><span class="sxs-lookup"><span data-stu-id="d6dae-213">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="d6dae-214">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span><span class="sxs-lookup"><span data-stu-id="d6dae-214">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="d6dae-215">Run one of the following commands to search for a specific user:</span><span class="sxs-lookup"><span data-stu-id="d6dae-215">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="d6dae-216">Here are a couple of examples:</span><span class="sxs-lookup"><span data-stu-id="d6dae-216">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="d6dae-217">Delete users</span><span class="sxs-lookup"><span data-stu-id="d6dae-217">Delete users</span></span>
<span data-ttu-id="d6dae-218">The process for deleting a user is straightforward.</span><span class="sxs-lookup"><span data-stu-id="d6dae-218">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="d6dae-219">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span><span class="sxs-lookup"><span data-stu-id="d6dae-219">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d6dae-220">To see an example, enter this command and view the delete request that is printed to the console:</span><span class="sxs-lookup"><span data-stu-id="d6dae-220">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="d6dae-221">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span><span class="sxs-lookup"><span data-stu-id="d6dae-221">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="d6dae-222">You can perform many other actions with the Azure AD Graph API in addition to user management.</span><span class="sxs-lookup"><span data-stu-id="d6dae-222">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="d6dae-223">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span><span class="sxs-lookup"><span data-stu-id="d6dae-223">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="d6dae-224">Use custom attributes</span><span class="sxs-lookup"><span data-stu-id="d6dae-224">Use custom attributes</span></span>
<span data-ttu-id="d6dae-225">Most consumer applications need to store some type of custom user profile information.</span><span class="sxs-lookup"><span data-stu-id="d6dae-225">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="d6dae-226">One way you can do this is to define a custom attribute in your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-226">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="d6dae-227">You can then treat that attribute the same way you treat any other property on a user object.</span><span class="sxs-lookup"><span data-stu-id="d6dae-227">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="d6dae-228">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="d6dae-228">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="d6dae-229">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="d6dae-229">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="d6dae-230">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="d6dae-230">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="d6dae-231">The output of these functions reveals the details of each custom attribute, such as:</span><span class="sxs-lookup"><span data-stu-id="d6dae-231">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="d6dae-232">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span><span class="sxs-lookup"><span data-stu-id="d6dae-232">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="d6dae-233">Update your .json file with the new property and a value for the property, and then run:</span><span class="sxs-lookup"><span data-stu-id="d6dae-233">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="d6dae-234">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span><span class="sxs-lookup"><span data-stu-id="d6dae-234">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="d6dae-235">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d6dae-235">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="d6dae-236">It also acquires tokens by using a client secret.</span><span class="sxs-lookup"><span data-stu-id="d6dae-236">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="d6dae-237">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span><span class="sxs-lookup"><span data-stu-id="d6dae-237">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="d6dae-238">You need to grant the application the proper permissions in the tenant.</span><span class="sxs-lookup"><span data-stu-id="d6dae-238">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="d6dae-239">For now, you need to use ADAL v2 to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="d6dae-239">For now, you need to use ADAL v2 to get access tokens.</span></span> <span data-ttu-id="d6dae-240">(You can also send protocol messages directly, without using a library.)</span><span class="sxs-lookup"><span data-stu-id="d6dae-240">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="d6dae-241">When you call the Graph API, use `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d6dae-241">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="d6dae-242">When you create and update consumer users, a few properties are required, as described above.</span><span class="sxs-lookup"><span data-stu-id="d6dae-242">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="d6dae-243">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span><span class="sxs-lookup"><span data-stu-id="d6dae-243">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

