---
title: User migration approaches in Azure Active Directory B2C | Microsoft Docs
description: Discuss core and advanced concepts on user migration using Graph API and optionally using Azure AD B2C custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 10/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 7805b238d42201b791e038964985f784fcf8d4ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856165"
---
# <a name="azure-active-directory-b2c-user-migration"></a><span data-ttu-id="7f859-103">Azure Active Directory B2C: User migration</span><span class="sxs-lookup"><span data-stu-id="7f859-103">Azure Active Directory B2C: User migration</span></span>
<span data-ttu-id="7f859-104">When you migrate your identity provider to Azure Active Directory B2C (Azure AD B2C), you might also need to migrate the user account.</span><span class="sxs-lookup"><span data-stu-id="7f859-104">When you migrate your identity provider to Azure Active Directory B2C (Azure AD B2C), you might also need to migrate the user account.</span></span> <span data-ttu-id="7f859-105">This article explains how to migrate existing user accounts from any identity provider to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7f859-105">This article explains how to migrate existing user accounts from any identity provider to Azure AD B2C.</span></span> <span data-ttu-id="7f859-106">The article is not meant to be prescriptive but, rather, it describes a few scenarios.</span><span class="sxs-lookup"><span data-stu-id="7f859-106">The article is not meant to be prescriptive but, rather, it describes a few scenarios.</span></span> <span data-ttu-id="7f859-107">The developer is responsible for the suitability of each approach.</span><span class="sxs-lookup"><span data-stu-id="7f859-107">The developer is responsible for the suitability of each approach.</span></span>

## <a name="user-migration-flows"></a><span data-ttu-id="7f859-108">User migration flows</span><span class="sxs-lookup"><span data-stu-id="7f859-108">User migration flows</span></span>
<span data-ttu-id="7f859-109">With Azure AD B2C, you can migrate users through [Azure AD Graph API][B2C-GraphQuickStart].</span><span class="sxs-lookup"><span data-stu-id="7f859-109">With Azure AD B2C, you can migrate users through [Azure AD Graph API][B2C-GraphQuickStart].</span></span> <span data-ttu-id="7f859-110">The user migration process falls into two flows:</span><span class="sxs-lookup"><span data-stu-id="7f859-110">The user migration process falls into two flows:</span></span>

* <span data-ttu-id="7f859-111">**Pre-migration**: This flow applies when you either have clear access to a user's credentials (user name and password) or the credentials are encrypted, but you can decrypt them.</span><span class="sxs-lookup"><span data-stu-id="7f859-111">**Pre-migration**: This flow applies when you either have clear access to a user's credentials (user name and password) or the credentials are encrypted, but you can decrypt them.</span></span> <span data-ttu-id="7f859-112">The pre-migration process involves reading the users from the old identity provider and creating new accounts in the Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="7f859-112">The pre-migration process involves reading the users from the old identity provider and creating new accounts in the Azure AD B2C directory.</span></span>

* <span data-ttu-id="7f859-113">**Pre-migration and password reset**: This flow applies when a user's password is not accessible.</span><span class="sxs-lookup"><span data-stu-id="7f859-113">**Pre-migration and password reset**: This flow applies when a user's password is not accessible.</span></span> <span data-ttu-id="7f859-114">For example:</span><span class="sxs-lookup"><span data-stu-id="7f859-114">For example:</span></span>
    * <span data-ttu-id="7f859-115">The password is stored in HASH format.</span><span class="sxs-lookup"><span data-stu-id="7f859-115">The password is stored in HASH format.</span></span>
    * <span data-ttu-id="7f859-116">The password is stored in an identity provider that you can't access.</span><span class="sxs-lookup"><span data-stu-id="7f859-116">The password is stored in an identity provider that you can't access.</span></span> <span data-ttu-id="7f859-117">Your old identity provider validates the user credential by calling a web service.</span><span class="sxs-lookup"><span data-stu-id="7f859-117">Your old identity provider validates the user credential by calling a web service.</span></span>

<span data-ttu-id="7f859-118">In both flows, you first run the pre-migration process, read the users from your old identity provider, and create new accounts in the Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="7f859-118">In both flows, you first run the pre-migration process, read the users from your old identity provider, and create new accounts in the Azure AD B2C directory.</span></span> <span data-ttu-id="7f859-119">If you do not have the password, you create the account by using a password that's generated randomly.</span><span class="sxs-lookup"><span data-stu-id="7f859-119">If you do not have the password, you create the account by using a password that's generated randomly.</span></span> <span data-ttu-id="7f859-120">You then ask the user to change the password or, when the user signs in for the first time, Azure AD B2C asks the user to reset it.</span><span class="sxs-lookup"><span data-stu-id="7f859-120">You then ask the user to change the password or, when the user signs in for the first time, Azure AD B2C asks the user to reset it.</span></span>

## <a name="password-policy"></a><span data-ttu-id="7f859-121">Password policy</span><span class="sxs-lookup"><span data-stu-id="7f859-121">Password policy</span></span>
<span data-ttu-id="7f859-122">The Azure AD B2C password policy (for local accounts) is based on Azure AD policy.</span><span class="sxs-lookup"><span data-stu-id="7f859-122">The Azure AD B2C password policy (for local accounts) is based on Azure AD policy.</span></span> <span data-ttu-id="7f859-123">The Azure AD B2C sign-up or sign-in and password reset policies use the "strong" password strength and doesn't expire any passwords.</span><span class="sxs-lookup"><span data-stu-id="7f859-123">The Azure AD B2C sign-up or sign-in and password reset policies use the "strong" password strength and doesn't expire any passwords.</span></span> <span data-ttu-id="7f859-124">For more information, see [Azure AD password policy][AD-PasswordPolicies].</span><span class="sxs-lookup"><span data-stu-id="7f859-124">For more information, see [Azure AD password policy][AD-PasswordPolicies].</span></span>

<span data-ttu-id="7f859-125">If the accounts that you want to migrate use a weaker password strength than the [strong password strength enforced by Azure AD B2C][AD-PasswordPolicies], you can disable the strong password requirement.</span><span class="sxs-lookup"><span data-stu-id="7f859-125">If the accounts that you want to migrate use a weaker password strength than the [strong password strength enforced by Azure AD B2C][AD-PasswordPolicies], you can disable the strong password requirement.</span></span> <span data-ttu-id="7f859-126">To change the default password policy, set the `passwordPolicies` property to `DisableStrongPassword`.</span><span class="sxs-lookup"><span data-stu-id="7f859-126">To change the default password policy, set the `passwordPolicies` property to `DisableStrongPassword`.</span></span> <span data-ttu-id="7f859-127">For example, you can modify the create user request as follows:</span><span class="sxs-lookup"><span data-stu-id="7f859-127">For example, you can modify the create user request as follows:</span></span>

```JSON
"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"
```

## <a name="step-1-use-azure-ad-graph-api-to-migrate-users"></a><span data-ttu-id="7f859-128">Step 1: Use Azure AD Graph API to migrate users</span><span class="sxs-lookup"><span data-stu-id="7f859-128">Step 1: Use Azure AD Graph API to migrate users</span></span>
<span data-ttu-id="7f859-129">You create the Azure AD B2C user account via Graph API (with the password or with a random password).</span><span class="sxs-lookup"><span data-stu-id="7f859-129">You create the Azure AD B2C user account via Graph API (with the password or with a random password).</span></span> <span data-ttu-id="7f859-130">This section describes the process of creating user accounts in the Azure AD B2C directory by using Graph API.</span><span class="sxs-lookup"><span data-stu-id="7f859-130">This section describes the process of creating user accounts in the Azure AD B2C directory by using Graph API.</span></span>

### <a name="step-11-register-your-application-in-your-tenant"></a><span data-ttu-id="7f859-131">Step 1.1: Register your application in your tenant</span><span class="sxs-lookup"><span data-stu-id="7f859-131">Step 1.1: Register your application in your tenant</span></span>
<span data-ttu-id="7f859-132">To communicate with the Graph API, you first must have a service account with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="7f859-132">To communicate with the Graph API, you first must have a service account with administrative privileges.</span></span> <span data-ttu-id="7f859-133">In Azure AD, you register an application and authentication to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f859-133">In Azure AD, you register an application and authentication to Azure AD.</span></span> <span data-ttu-id="7f859-134">The application credentials are **Application ID** and **Application Secret**.</span><span class="sxs-lookup"><span data-stu-id="7f859-134">The application credentials are **Application ID** and **Application Secret**.</span></span> <span data-ttu-id="7f859-135">The application acts as itself, not as a user, to call the Graph API.</span><span class="sxs-lookup"><span data-stu-id="7f859-135">The application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="7f859-136">First, register your migration application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f859-136">First, register your migration application in Azure AD.</span></span> <span data-ttu-id="7f859-137">Then, create an application key (application secret) and set the application with write privileges.</span><span class="sxs-lookup"><span data-stu-id="7f859-137">Then, create an application key (application secret) and set the application with write privileges.</span></span>

1. <span data-ttu-id="7f859-138">Sign in to the [Azure portal][Portal].</span><span class="sxs-lookup"><span data-stu-id="7f859-138">Sign in to the [Azure portal][Portal].</span></span>

2. <span data-ttu-id="7f859-139">Choose your Azure AD **B2C** tenant by selecting your account at the top right of the window.</span><span class="sxs-lookup"><span data-stu-id="7f859-139">Choose your Azure AD **B2C** tenant by selecting your account at the top right of the window.</span></span>

3. <span data-ttu-id="7f859-140">In the left pane, select **Azure Active Directory** (not Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7f859-140">In the left pane, select **Azure Active Directory** (not Azure AD B2C).</span></span> <span data-ttu-id="7f859-141">To find it, you might need to select **More Services**.</span><span class="sxs-lookup"><span data-stu-id="7f859-141">To find it, you might need to select **More Services**.</span></span>

4. <span data-ttu-id="7f859-142">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="7f859-142">Select **App registrations**.</span></span>

5. <span data-ttu-id="7f859-143">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="7f859-143">Select **New application registration**.</span></span>

    ![New application registration](media/active-directory-b2c-user-migration/pre-migration-app-registration.png)

6. <span data-ttu-id="7f859-145">Create a new application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="7f859-145">Create a new application by doing the following:</span></span>
    * <span data-ttu-id="7f859-146">For **Name**, use **B2CUserMigration** or any other name you want.</span><span class="sxs-lookup"><span data-stu-id="7f859-146">For **Name**, use **B2CUserMigration** or any other name you want.</span></span>
    * <span data-ttu-id="7f859-147">For **Application type**, use **Web app/API**.</span><span class="sxs-lookup"><span data-stu-id="7f859-147">For **Application type**, use **Web app/API**.</span></span>
    * <span data-ttu-id="7f859-148">For **Sign-on URL**, use **https://localhost** (as it's not relevant for this application).</span><span class="sxs-lookup"><span data-stu-id="7f859-148">For **Sign-on URL**, use **https://localhost** (as it's not relevant for this application).</span></span>
    * <span data-ttu-id="7f859-149">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f859-149">Select **Create**.</span></span>

7. <span data-ttu-id="7f859-150">After the application is created, in the **Applications** list, select the newly created **B2CUserMigration** application.</span><span class="sxs-lookup"><span data-stu-id="7f859-150">After the application is created, in the **Applications** list, select the newly created **B2CUserMigration** application.</span></span>

8. <span data-ttu-id="7f859-151">Select **Properties**, copy the **Application ID**, and save it for later.</span><span class="sxs-lookup"><span data-stu-id="7f859-151">Select **Properties**, copy the **Application ID**, and save it for later.</span></span>

### <a name="step-12-create-the-application-secret"></a><span data-ttu-id="7f859-152">Step 1.2: Create the application secret</span><span class="sxs-lookup"><span data-stu-id="7f859-152">Step 1.2: Create the application secret</span></span>
1. <span data-ttu-id="7f859-153">In the Azure portal **Registered App** window, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="7f859-153">In the Azure portal **Registered App** window, select **Keys**.</span></span>

2. <span data-ttu-id="7f859-154">Add a new key (also known as a client secret), and then copy the key for later use.</span><span class="sxs-lookup"><span data-stu-id="7f859-154">Add a new key (also known as a client secret), and then copy the key for later use.</span></span>

    ![Application ID and Keys](media/active-directory-b2c-user-migration/pre-migration-app-id-and-key.png)

### <a name="step-13-grant-administrative-permission-to-your-application"></a><span data-ttu-id="7f859-156">Step 1.3: Grant administrative permission to your application</span><span class="sxs-lookup"><span data-stu-id="7f859-156">Step 1.3: Grant administrative permission to your application</span></span>
1. <span data-ttu-id="7f859-157">In the Azure portal **Registered App** window, select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="7f859-157">In the Azure portal **Registered App** window, select **Required permissions**.</span></span>

2. <span data-ttu-id="7f859-158">Select **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f859-158">Select **Windows Azure Active Directory**.</span></span>

3. <span data-ttu-id="7f859-159">In the **Enable Access** pane, under **Application Permissions**, select **Read and write directory data**, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="7f859-159">In the **Enable Access** pane, under **Application Permissions**, select **Read and write directory data**, and then select **Save**.</span></span>

4. <span data-ttu-id="7f859-160">In the **Required permissions** pane, select **Grant Permissions**.</span><span class="sxs-lookup"><span data-stu-id="7f859-160">In the **Required permissions** pane, select **Grant Permissions**.</span></span>

    ![Application permissions](media/active-directory-b2c-user-migration/pre-migration-app-registration-permissions.png)

<span data-ttu-id="7f859-162">Now you have an application with permissions to create, read, and update users from your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7f859-162">Now you have an application with permissions to create, read, and update users from your Azure AD B2C tenant.</span></span>

### <a name="step-14-optional-environment-cleanup"></a><span data-ttu-id="7f859-163">Step 1.4: (Optional) Environment cleanup</span><span class="sxs-lookup"><span data-stu-id="7f859-163">Step 1.4: (Optional) Environment cleanup</span></span>
<span data-ttu-id="7f859-164">Read and write directory data permissions do *not* include the right to delete users.</span><span class="sxs-lookup"><span data-stu-id="7f859-164">Read and write directory data permissions do *not* include the right to delete users.</span></span> <span data-ttu-id="7f859-165">To give your application the ability to delete users (to clean up your environment), you must perform an extra step, which involves running PowerShell to set User Account Administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="7f859-165">To give your application the ability to delete users (to clean up your environment), you must perform an extra step, which involves running PowerShell to set User Account Administrator permissions.</span></span> <span data-ttu-id="7f859-166">Otherwise, you can skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="7f859-166">Otherwise, you can skip to the next section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f859-167">You must use a B2C tenant administrator account that is *local* to the B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7f859-167">You must use a B2C tenant administrator account that is *local* to the B2C tenant.</span></span> <span data-ttu-id="7f859-168">The account name syntax is *admin@contosob2c.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="7f859-168">The account name syntax is *admin@contosob2c.onmicrosoft.com*.</span></span>

>[!NOTE]
> <span data-ttu-id="7f859-169">The following PowerShell script requires [Azure Active Directory PowerShell Version 2][AD-Powershell].</span><span class="sxs-lookup"><span data-stu-id="7f859-169">The following PowerShell script requires [Azure Active Directory PowerShell Version 2][AD-Powershell].</span></span>

<span data-ttu-id="7f859-170">In this PowerShell script, do the following:</span><span class="sxs-lookup"><span data-stu-id="7f859-170">In this PowerShell script, do the following:</span></span>
1. <span data-ttu-id="7f859-171">Connect to your online service.</span><span class="sxs-lookup"><span data-stu-id="7f859-171">Connect to your online service.</span></span> <span data-ttu-id="7f859-172">To do so, run the `Connect-AzureAD` cmdlet at the Windows PowerShell command prompt, and provide your credentials.</span><span class="sxs-lookup"><span data-stu-id="7f859-172">To do so, run the `Connect-AzureAD` cmdlet at the Windows PowerShell command prompt, and provide your credentials.</span></span>

2. <span data-ttu-id="7f859-173">Use the **Application ID** to assign the application the user account administrator role.</span><span class="sxs-lookup"><span data-stu-id="7f859-173">Use the **Application ID** to assign the application the user account administrator role.</span></span> <span data-ttu-id="7f859-174">These roles have well-known identifiers, so all you need to do is enter your **Application ID** in the script.</span><span class="sxs-lookup"><span data-stu-id="7f859-174">These roles have well-known identifiers, so all you need to do is enter your **Application ID** in the script.</span></span>

```PowerShell
Connect-AzureAD

$AppId = "<Your application ID>"

# Fetch Azure AD application to assign to role
$roleMember = Get-AzureADServicePrincipal -Filter "AppId eq '$AppId'"

# Fetch User Account Administrator role instance
$role = Get-AzureADDirectoryRole | Where-Object {$_.displayName -eq 'User Account Administrator'}

# If role instance does not exist, instantiate it based on the role template
if ($role -eq $null) {
    # Instantiate an instance of the role template
    $roleTemplate = Get-AzureADDirectoryRoleTemplate | Where-Object {$_.displayName -eq 'User Account Administrator'}
    Enable-AzureADDirectoryRole -RoleTemplateId $roleTemplate.ObjectId

    # Fetch User Account Administrator role instance again
    $role = Get-AzureADDirectoryRole | Where-Object {$_.displayName -eq 'User Account Administrator'}
}

# Add application to role
Add-AzureADDirectoryRoleMember -ObjectId $role.ObjectId -RefObjectId $roleMember.ObjectId

# Fetch role membership for role to confirm
Get-AzureADDirectoryRoleMember -ObjectId $role.ObjectId
```

<span data-ttu-id="7f859-175">Change the `$AppId` value with your Azure AD **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="7f859-175">Change the `$AppId` value with your Azure AD **Application ID**.</span></span>

## <a name="step-2-pre-migration-application-sample"></a><span data-ttu-id="7f859-176">Step 2: Pre-migration application sample</span><span class="sxs-lookup"><span data-stu-id="7f859-176">Step 2: Pre-migration application sample</span></span>
<span data-ttu-id="7f859-177">[Download and run the sample code][UserMigrationSample].</span><span class="sxs-lookup"><span data-stu-id="7f859-177">[Download and run the sample code][UserMigrationSample].</span></span> <span data-ttu-id="7f859-178">You can download it as a .zip file.</span><span class="sxs-lookup"><span data-stu-id="7f859-178">You can download it as a .zip file.</span></span>

### <a name="step-21-edit-the-migration-data-file"></a><span data-ttu-id="7f859-179">Step 2.1: Edit the migration data file</span><span class="sxs-lookup"><span data-stu-id="7f859-179">Step 2.1: Edit the migration data file</span></span>
<span data-ttu-id="7f859-180">The sample app uses a JSON file that contains dummy user data.</span><span class="sxs-lookup"><span data-stu-id="7f859-180">The sample app uses a JSON file that contains dummy user data.</span></span> <span data-ttu-id="7f859-181">After you successfully run the sample, you can change the code to consume the data from your own database.</span><span class="sxs-lookup"><span data-stu-id="7f859-181">After you successfully run the sample, you can change the code to consume the data from your own database.</span></span> <span data-ttu-id="7f859-182">Or you can export the user profile to a JSON file, and then set the app to use that file.</span><span class="sxs-lookup"><span data-stu-id="7f859-182">Or you can export the user profile to a JSON file, and then set the app to use that file.</span></span>

<span data-ttu-id="7f859-183">To edit the JSON file, open the `AADB2C.UserMigration.sln` Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="7f859-183">To edit the JSON file, open the `AADB2C.UserMigration.sln` Visual Studio solution.</span></span> <span data-ttu-id="7f859-184">In the `AADB2C.UserMigration` project, open the `UsersData.json` file.</span><span class="sxs-lookup"><span data-stu-id="7f859-184">In the `AADB2C.UserMigration` project, open the `UsersData.json` file.</span></span>

![User data file](media/active-directory-b2c-user-migration/pre-migration-data-file.png)

<span data-ttu-id="7f859-186">As you can see, the file contains a list of user entities.</span><span class="sxs-lookup"><span data-stu-id="7f859-186">As you can see, the file contains a list of user entities.</span></span> <span data-ttu-id="7f859-187">Each user entity has the following properties:</span><span class="sxs-lookup"><span data-stu-id="7f859-187">Each user entity has the following properties:</span></span>
* <span data-ttu-id="7f859-188">email</span><span class="sxs-lookup"><span data-stu-id="7f859-188">email</span></span>
* <span data-ttu-id="7f859-189">displayName</span><span class="sxs-lookup"><span data-stu-id="7f859-189">displayName</span></span>
* <span data-ttu-id="7f859-190">firstName</span><span class="sxs-lookup"><span data-stu-id="7f859-190">firstName</span></span>
* <span data-ttu-id="7f859-191">lastName</span><span class="sxs-lookup"><span data-stu-id="7f859-191">lastName</span></span>
* <span data-ttu-id="7f859-192">password (can be empty)</span><span class="sxs-lookup"><span data-stu-id="7f859-192">password (can be empty)</span></span>

> [!NOTE]
> <span data-ttu-id="7f859-193">At compile time, Visual Studio copies the file to the `bin` directory.</span><span class="sxs-lookup"><span data-stu-id="7f859-193">At compile time, Visual Studio copies the file to the `bin` directory.</span></span>

### <a name="step-22-configure-the-application-settings"></a><span data-ttu-id="7f859-194">Step 2.2: Configure the application settings</span><span class="sxs-lookup"><span data-stu-id="7f859-194">Step 2.2: Configure the application settings</span></span>
<span data-ttu-id="7f859-195">Under the `AADB2C.UserMigration` project, open the *App.config* file.</span><span class="sxs-lookup"><span data-stu-id="7f859-195">Under the `AADB2C.UserMigration` project, open the *App.config* file.</span></span> <span data-ttu-id="7f859-196">Replace the following app settings with your own values:</span><span class="sxs-lookup"><span data-stu-id="7f859-196">Replace the following app settings with your own values:</span></span>

```XML
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Client Secret Key from above}" />
    <add key="MigrationFile" value="{Name of a JSON file containing the users' data; for example, UsersData.json}" />
    <add key="BlobStorageConnectionString" value="{Your connection Azure table string}" />
</appSettings>
```

> [!NOTE]
> * <span data-ttu-id="7f859-197">The use of an Azure table connection string is described in the next sections.</span><span class="sxs-lookup"><span data-stu-id="7f859-197">The use of an Azure table connection string is described in the next sections.</span></span>
> * <span data-ttu-id="7f859-198">Your B2C tenant name is the domain that you entered during tenant creation, and it is displayed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f859-198">Your B2C tenant name is the domain that you entered during tenant creation, and it is displayed in the Azure portal.</span></span> <span data-ttu-id="7f859-199">The tenant name usually ends with the suffix *.onmicrosoft.com* (for example, *contosob2c.onmicrosoft.com*).</span><span class="sxs-lookup"><span data-stu-id="7f859-199">The tenant name usually ends with the suffix *.onmicrosoft.com* (for example, *contosob2c.onmicrosoft.com*).</span></span>
>

### <a name="step-23-run-the-pre-migration-process"></a><span data-ttu-id="7f859-200">Step 2.3: Run the pre-migration process</span><span class="sxs-lookup"><span data-stu-id="7f859-200">Step 2.3: Run the pre-migration process</span></span>
<span data-ttu-id="7f859-201">Right-click the `AADB2C.UserMigration` solution, and then rebuild the sample.</span><span class="sxs-lookup"><span data-stu-id="7f859-201">Right-click the `AADB2C.UserMigration` solution, and then rebuild the sample.</span></span> <span data-ttu-id="7f859-202">If you are successful, you should now have a `UserMigration.exe` executable file located in `AADB2C.UserMigration\bin\Debug\net461`.</span><span class="sxs-lookup"><span data-stu-id="7f859-202">If you are successful, you should now have a `UserMigration.exe` executable file located in `AADB2C.UserMigration\bin\Debug\net461`.</span></span> <span data-ttu-id="7f859-203">To run the migration process, use one of the following command-line parameters:</span><span class="sxs-lookup"><span data-stu-id="7f859-203">To run the migration process, use one of the following command-line parameters:</span></span>

* <span data-ttu-id="7f859-204">To **migrate users with password**, use the `UserMigration.exe 1` command.</span><span class="sxs-lookup"><span data-stu-id="7f859-204">To **migrate users with password**, use the `UserMigration.exe 1` command.</span></span>

* <span data-ttu-id="7f859-205">To **migrate users with random password**, use the `UserMigration.exe 2` command.</span><span class="sxs-lookup"><span data-stu-id="7f859-205">To **migrate users with random password**, use the `UserMigration.exe 2` command.</span></span> <span data-ttu-id="7f859-206">This operation also creates an Azure table entity.</span><span class="sxs-lookup"><span data-stu-id="7f859-206">This operation also creates an Azure table entity.</span></span> <span data-ttu-id="7f859-207">Later, you configure the policy to call the REST API service.</span><span class="sxs-lookup"><span data-stu-id="7f859-207">Later, you configure the policy to call the REST API service.</span></span> <span data-ttu-id="7f859-208">The service uses an Azure table to track and manage the migration process.</span><span class="sxs-lookup"><span data-stu-id="7f859-208">The service uses an Azure table to track and manage the migration process.</span></span>

![Migration process demo](media/active-directory-b2c-user-migration/pre-migration-demo.png)

### <a name="step-24-check-the-pre-migration-process"></a><span data-ttu-id="7f859-210">Step 2.4: Check the pre-migration process</span><span class="sxs-lookup"><span data-stu-id="7f859-210">Step 2.4: Check the pre-migration process</span></span>
<span data-ttu-id="7f859-211">To validate the migration, use one of the following two methods:</span><span class="sxs-lookup"><span data-stu-id="7f859-211">To validate the migration, use one of the following two methods:</span></span>

* <span data-ttu-id="7f859-212">To search for a user by display name, use the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="7f859-212">To search for a user by display name, use the Azure portal:</span></span>

    <span data-ttu-id="7f859-213">a.</span><span class="sxs-lookup"><span data-stu-id="7f859-213">a.</span></span> <span data-ttu-id="7f859-214">Open **Azure AD B2C**, and then select **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="7f859-214">Open **Azure AD B2C**, and then select **Users and Groups**.</span></span>

    <span data-ttu-id="7f859-215">b.</span><span class="sxs-lookup"><span data-stu-id="7f859-215">b.</span></span> <span data-ttu-id="7f859-216">In the search box, type the user's display name, and then view the user's profile.</span><span class="sxs-lookup"><span data-stu-id="7f859-216">In the search box, type the user's display name, and then view the user's profile.</span></span>

* <span data-ttu-id="7f859-217">To retrieve a user by sign-in email address, use this sample application:</span><span class="sxs-lookup"><span data-stu-id="7f859-217">To retrieve a user by sign-in email address, use this sample application:</span></span>

    <span data-ttu-id="7f859-218">a.</span><span class="sxs-lookup"><span data-stu-id="7f859-218">a.</span></span> <span data-ttu-id="7f859-219">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="7f859-219">Run the following command:</span></span>

    ```Console
        UserMigration.exe 3 {email address}
    ```

    > [!TIP]
    > <span data-ttu-id="7f859-220">You can also retrieve a user by display name by using the following command: `UserMigration.exe 4 "<Display name>"`.</span><span class="sxs-lookup"><span data-stu-id="7f859-220">You can also retrieve a user by display name by using the following command: `UserMigration.exe 4 "<Display name>"`.</span></span>

    <span data-ttu-id="7f859-221">b.</span><span class="sxs-lookup"><span data-stu-id="7f859-221">b.</span></span> <span data-ttu-id="7f859-222">Open the UserProfile.json file in a JSON editor to see user's information.</span><span class="sxs-lookup"><span data-stu-id="7f859-222">Open the UserProfile.json file in a JSON editor to see user's information.</span></span>

    ![The UserProfile.json file](media/active-directory-b2c-user-migration/pre-migration-get-by-email2.png)

### <a name="step-25-optional-environment-cleanup"></a><span data-ttu-id="7f859-224">Step 2.5: (Optional) Environment cleanup</span><span class="sxs-lookup"><span data-stu-id="7f859-224">Step 2.5: (Optional) Environment cleanup</span></span>
<span data-ttu-id="7f859-225">If you want to clean up your Azure AD tenant and remove users from the Azure AD directory, run the `UserMigration.exe 5` command.</span><span class="sxs-lookup"><span data-stu-id="7f859-225">If you want to clean up your Azure AD tenant and remove users from the Azure AD directory, run the `UserMigration.exe 5` command.</span></span>

> [!NOTE]
> * <span data-ttu-id="7f859-226">To clean up your tenant, configure User Account Administrator permissions for your application.</span><span class="sxs-lookup"><span data-stu-id="7f859-226">To clean up your tenant, configure User Account Administrator permissions for your application.</span></span>
> * <span data-ttu-id="7f859-227">The sample migration app cleans up all users who are listed in the JSON file.</span><span class="sxs-lookup"><span data-stu-id="7f859-227">The sample migration app cleans up all users who are listed in the JSON file.</span></span>

### <a name="step-26-sign-in-with-migrated-users-with-password"></a><span data-ttu-id="7f859-228">Step 2.6: Sign in with migrated users (with password)</span><span class="sxs-lookup"><span data-stu-id="7f859-228">Step 2.6: Sign in with migrated users (with password)</span></span>
<span data-ttu-id="7f859-229">After you run the pre-migration process with user passwords, the accounts are ready to use, and users can sign in to your application by using Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7f859-229">After you run the pre-migration process with user passwords, the accounts are ready to use, and users can sign in to your application by using Azure AD B2C.</span></span> <span data-ttu-id="7f859-230">If you don't have access to user passwords, continue to the next section.</span><span class="sxs-lookup"><span data-stu-id="7f859-230">If you don't have access to user passwords, continue to the next section.</span></span>

## <a name="step-3-help-users-reset-their-password"></a><span data-ttu-id="7f859-231">Step 3: Help users reset their password</span><span class="sxs-lookup"><span data-stu-id="7f859-231">Step 3: Help users reset their password</span></span>
<span data-ttu-id="7f859-232">If you migrate users with a random password, they must reset their password.</span><span class="sxs-lookup"><span data-stu-id="7f859-232">If you migrate users with a random password, they must reset their password.</span></span> <span data-ttu-id="7f859-233">To help them reset the password, send a welcome email with a link to reset the password.</span><span class="sxs-lookup"><span data-stu-id="7f859-233">To help them reset the password, send a welcome email with a link to reset the password.</span></span>

<span data-ttu-id="7f859-234">To get the link to your password reset policy, do the following:</span><span class="sxs-lookup"><span data-stu-id="7f859-234">To get the link to your password reset policy, do the following:</span></span>

1. <span data-ttu-id="7f859-235">Select **Azure AD B2C Settings**, and then select **Reset password** policy properties.</span><span class="sxs-lookup"><span data-stu-id="7f859-235">Select **Azure AD B2C Settings**, and then select **Reset password** policy properties.</span></span>

2. <span data-ttu-id="7f859-236">Select your application.</span><span class="sxs-lookup"><span data-stu-id="7f859-236">Select your application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f859-237">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="7f859-237">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="7f859-238">To learn how to register applications, see the Azure AD B2C [Get started][B2C-GetStarted] article or the [Application registration][B2C-AppRegister] article.</span><span class="sxs-lookup"><span data-stu-id="7f859-238">To learn how to register applications, see the Azure AD B2C [Get started][B2C-GetStarted] article or the [Application registration][B2C-AppRegister] article.</span></span>

3. <span data-ttu-id="7f859-239">Select **Run now**, and then check the policy.</span><span class="sxs-lookup"><span data-stu-id="7f859-239">Select **Run now**, and then check the policy.</span></span>

4. <span data-ttu-id="7f859-240">In the **Run now endpoint** box, copy the URL, and then send it to your users.</span><span class="sxs-lookup"><span data-stu-id="7f859-240">In the **Run now endpoint** box, copy the URL, and then send it to your users.</span></span>

    ![Set diagnostics logs](media/active-directory-b2c-user-migration/pre-migration-policy-uri.png)

## <a name="step-4-optional-change-your-policy-to-check-and-set-the-user-migration-status"></a><span data-ttu-id="7f859-242">Step 4: (Optional) Change your policy to check and set the user migration status</span><span class="sxs-lookup"><span data-stu-id="7f859-242">Step 4: (Optional) Change your policy to check and set the user migration status</span></span>

> [!NOTE]
> <span data-ttu-id="7f859-243">To check and change the user migration status, you must use a custom policy.</span><span class="sxs-lookup"><span data-stu-id="7f859-243">To check and change the user migration status, you must use a custom policy.</span></span> <span data-ttu-id="7f859-244">The set-up instructions from [Get started with custom policies][B2C-GetStartedCustom] must be completed.</span><span class="sxs-lookup"><span data-stu-id="7f859-244">The set-up instructions from [Get started with custom policies][B2C-GetStartedCustom] must be completed.</span></span>
>

<span data-ttu-id="7f859-245">When users try to sign in without resetting the password first, your policy should return a friendly error message.</span><span class="sxs-lookup"><span data-stu-id="7f859-245">When users try to sign in without resetting the password first, your policy should return a friendly error message.</span></span> <span data-ttu-id="7f859-246">For example:</span><span class="sxs-lookup"><span data-stu-id="7f859-246">For example:</span></span>
><span data-ttu-id="7f859-247">*Your password has expired. To reset it, select the Reset Password link.*</span><span class="sxs-lookup"><span data-stu-id="7f859-247">*Your password has expired. To reset it, select the Reset Password link.*</span></span>

<span data-ttu-id="7f859-248">This optional step requires the use of Azure AD B2C custom policies, as described in the [Getting started with custom policies][B2C-GetStartedCustom] article.</span><span class="sxs-lookup"><span data-stu-id="7f859-248">This optional step requires the use of Azure AD B2C custom policies, as described in the [Getting started with custom policies][B2C-GetStartedCustom] article.</span></span>

<span data-ttu-id="7f859-249">In this section, you change the policy to check the user migration status on sign-in.</span><span class="sxs-lookup"><span data-stu-id="7f859-249">In this section, you change the policy to check the user migration status on sign-in.</span></span> <span data-ttu-id="7f859-250">If the user didn't change the password, return an HTTP 409 error message that asks the user to select the **Forgot your password?** link.</span><span class="sxs-lookup"><span data-stu-id="7f859-250">If the user didn't change the password, return an HTTP 409 error message that asks the user to select the **Forgot your password?** link.</span></span>

<span data-ttu-id="7f859-251">To track the password change, you use an Azure table.</span><span class="sxs-lookup"><span data-stu-id="7f859-251">To track the password change, you use an Azure table.</span></span> <span data-ttu-id="7f859-252">When you run the pre-migration process with the command-line parameter `2`, you create a user entity in an Azure table.</span><span class="sxs-lookup"><span data-stu-id="7f859-252">When you run the pre-migration process with the command-line parameter `2`, you create a user entity in an Azure table.</span></span> <span data-ttu-id="7f859-253">Your service does the following:</span><span class="sxs-lookup"><span data-stu-id="7f859-253">Your service does the following:</span></span>

* <span data-ttu-id="7f859-254">On sign-in, the Azure AD B2C policy invokes your migration RESTful service, sending an email message as an input claim.</span><span class="sxs-lookup"><span data-stu-id="7f859-254">On sign-in, the Azure AD B2C policy invokes your migration RESTful service, sending an email message as an input claim.</span></span> <span data-ttu-id="7f859-255">The service searches for the email address in the Azure table.</span><span class="sxs-lookup"><span data-stu-id="7f859-255">The service searches for the email address in the Azure table.</span></span> <span data-ttu-id="7f859-256">If the address exists, the service throws an error message: *You must change password*.</span><span class="sxs-lookup"><span data-stu-id="7f859-256">If the address exists, the service throws an error message: *You must change password*.</span></span>

* <span data-ttu-id="7f859-257">After the user successfully changes the password, remove the entity from the Azure table.</span><span class="sxs-lookup"><span data-stu-id="7f859-257">After the user successfully changes the password, remove the entity from the Azure table.</span></span>

>[!NOTE]
><span data-ttu-id="7f859-258">We use an Azure table to simplify the sample.</span><span class="sxs-lookup"><span data-stu-id="7f859-258">We use an Azure table to simplify the sample.</span></span> <span data-ttu-id="7f859-259">You can store the migration status in any database or as a custom property in the Azure AD B2C account.</span><span class="sxs-lookup"><span data-stu-id="7f859-259">You can store the migration status in any database or as a custom property in the Azure AD B2C account.</span></span>

### <a name="41-update-your-application-setting"></a><span data-ttu-id="7f859-260">4.1: Update your application setting</span><span class="sxs-lookup"><span data-stu-id="7f859-260">4.1: Update your application setting</span></span>
1. <span data-ttu-id="7f859-261">To test the RESTful API demo, open `AADB2C.UserMigration.sln` in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f859-261">To test the RESTful API demo, open `AADB2C.UserMigration.sln` in Visual Studio.</span></span>

2. <span data-ttu-id="7f859-262">In the `AADB2C.UserMigration.API` project, open the *appsettings.json* file.</span><span class="sxs-lookup"><span data-stu-id="7f859-262">In the `AADB2C.UserMigration.API` project, open the *appsettings.json* file.</span></span> <span data-ttu-id="7f859-263">Replace the setting with the one configured in [Step 2.2](#step-22-configure-the-application-settings):</span><span class="sxs-lookup"><span data-stu-id="7f859-263">Replace the setting with the one configured in [Step 2.2](#step-22-configure-the-application-settings):</span></span>

    ```json
    {
        "BlobStorageConnectionString": "{The Azure Blob storage connection string}",
        ...
    }
    ```

### <a name="step-42-deploy-your-web-application-to-azure-app-service"></a><span data-ttu-id="7f859-264">Step 4.2: Deploy your web application to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7f859-264">Step 4.2: Deploy your web application to Azure App Service</span></span>
<span data-ttu-id="7f859-265">In Solution Explorer, right-click on the `AADB2C.UserMigration.API`, select "Publish...".</span><span class="sxs-lookup"><span data-stu-id="7f859-265">In Solution Explorer, right-click on the `AADB2C.UserMigration.API`, select "Publish...".</span></span> <span data-ttu-id="7f859-266">Follow the instructions to publish to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7f859-266">Follow the instructions to publish to Azure App Service.</span></span> <span data-ttu-id="7f859-267">For more information, see [Deploy your app to Azure App Service][AppService-Deploy].</span><span class="sxs-lookup"><span data-stu-id="7f859-267">For more information, see [Deploy your app to Azure App Service][AppService-Deploy].</span></span>

### <a name="step-43-add-a-technical-profile-and-technical-profile-validation-to-your-policy"></a><span data-ttu-id="7f859-268">Step 4.3: Add a technical profile and technical profile validation to your policy</span><span class="sxs-lookup"><span data-stu-id="7f859-268">Step 4.3: Add a technical profile and technical profile validation to your policy</span></span>
1. <span data-ttu-id="7f859-269">In Solution Explorer, expand "Solution Items", and open the *TrustFrameworkExtensions.xml* policy file.</span><span class="sxs-lookup"><span data-stu-id="7f859-269">In Solution Explorer, expand "Solution Items", and open the *TrustFrameworkExtensions.xml* policy file.</span></span>
2. <span data-ttu-id="7f859-270">Change `TenantId`, `PublicPolicyUri` and `<TenantId>` fields from `yourtenant.onmicrosoft.com` to the name of your tenant.</span><span class="sxs-lookup"><span data-stu-id="7f859-270">Change `TenantId`, `PublicPolicyUri` and `<TenantId>` fields from `yourtenant.onmicrosoft.com` to the name of your tenant.</span></span>
3. <span data-ttu-id="7f859-271">Under the `<TechnicalProfile Id="login-NonInteractive">` element, replace all instances of `ProxyIdentityExperienceFrameworkAppId` and `IdentityExperienceFrameworkAppId` with the Application IDs configured in [Getting started with custom policies][B2C-GetStartedCustom].</span><span class="sxs-lookup"><span data-stu-id="7f859-271">Under the `<TechnicalProfile Id="login-NonInteractive">` element, replace all instances of `ProxyIdentityExperienceFrameworkAppId` and `IdentityExperienceFrameworkAppId` with the Application IDs configured in [Getting started with custom policies][B2C-GetStartedCustom].</span></span>
4. <span data-ttu-id="7f859-272">Under the `<ClaimsProviders>` node, find the following XML snippet.</span><span class="sxs-lookup"><span data-stu-id="7f859-272">Under the `<ClaimsProviders>` node, find the following XML snippet.</span></span> <span data-ttu-id="7f859-273">Change the value of `ServiceUrl` to point to your Azure App Service URL.</span><span class="sxs-lookup"><span data-stu-id="7f859-273">Change the value of `ServiceUrl` to point to your Azure App Service URL.</span></span>

    ```XML
    <ClaimsProvider>
      <DisplayName>REST APIs</DisplayName>
      <TechnicalProfiles>

        <TechnicalProfile Id="LocalAccountSignIn">
          <DisplayName>Local account just in time migration</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ServiceUrl">http://{your-app}.azurewebsites.net/api/PrePasswordReset/LoalAccountSignIn</Item>
            <Item Key="AuthenticationType">None</Item>
            <Item Key="SendClaimsIn">Body</Item>
          </Metadata>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="signInName" PartnerClaimType="email" />
          </InputClaims>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>

        <TechnicalProfile Id="LocalAccountPasswordReset">
          <DisplayName>Local account just in time migration</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ServiceUrl">http://{your-app}.azurewebsites.net/api/PrePasswordReset/PasswordUpdated</Item>
            <Item Key="AuthenticationType">None</Item>
            <Item Key="SendClaimsIn">Body</Item>
          </Metadata>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
          </InputClaims>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

<span data-ttu-id="7f859-274">The preceding technical profile defines one input claim: `signInName` (send as email).</span><span class="sxs-lookup"><span data-stu-id="7f859-274">The preceding technical profile defines one input claim: `signInName` (send as email).</span></span> <span data-ttu-id="7f859-275">On sign-in, the claim is sent to your RESTful endpoint.</span><span class="sxs-lookup"><span data-stu-id="7f859-275">On sign-in, the claim is sent to your RESTful endpoint.</span></span>

<span data-ttu-id="7f859-276">After you define the technical profile for your RESTful API, tell your Azure AD B2C policy to call the technical profile.</span><span class="sxs-lookup"><span data-stu-id="7f859-276">After you define the technical profile for your RESTful API, tell your Azure AD B2C policy to call the technical profile.</span></span> <span data-ttu-id="7f859-277">The XML snippet overrides `SelfAsserted-LocalAccountSignin-Email`, which is defined in the base policy.</span><span class="sxs-lookup"><span data-stu-id="7f859-277">The XML snippet overrides `SelfAsserted-LocalAccountSignin-Email`, which is defined in the base policy.</span></span> <span data-ttu-id="7f859-278">The XML snippet also adds `ValidationTechnicalProfile`, with ReferenceId pointing to your technical profile `LocalAccountUserMigration`.</span><span class="sxs-lookup"><span data-stu-id="7f859-278">The XML snippet also adds `ValidationTechnicalProfile`, with ReferenceId pointing to your technical profile `LocalAccountUserMigration`.</span></span>

### <a name="step-44-upload-the-policy-to-your-tenant"></a><span data-ttu-id="7f859-279">Step 4.4: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="7f859-279">Step 4.4: Upload the policy to your tenant</span></span>
1. <span data-ttu-id="7f859-280">In the [Azure portal][Portal], switch to the [context of your Azure AD B2C tenant][B2C-NavContext], and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="7f859-280">In the [Azure portal][Portal], switch to the [context of your Azure AD B2C tenant][B2C-NavContext], and then select **Azure AD B2C**.</span></span>

2. <span data-ttu-id="7f859-281">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="7f859-281">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="7f859-282">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="7f859-282">Select **All Policies**.</span></span>

4. <span data-ttu-id="7f859-283">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="7f859-283">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="7f859-284">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="7f859-284">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="7f859-285">Upload the *TrustFrameworkExtensions.xml* file, and ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="7f859-285">Upload the *TrustFrameworkExtensions.xml* file, and ensure that it passes validation.</span></span>

### <a name="step-45-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="7f859-286">Step 4.5: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="7f859-286">Step 4.5: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="7f859-287">Select **Azure AD B2C Settings**, and then go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="7f859-287">Select **Azure AD B2C Settings**, and then go to **Identity Experience Framework**.</span></span>

2. <span data-ttu-id="7f859-288">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="7f859-288">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>

3. <span data-ttu-id="7f859-289">Try to sign in with one of the migrated users' credentials, and then select **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="7f859-289">Try to sign in with one of the migrated users' credentials, and then select **Sign In**.</span></span> <span data-ttu-id="7f859-290">Your REST API should throw the following error message:</span><span class="sxs-lookup"><span data-stu-id="7f859-290">Your REST API should throw the following error message:</span></span>

    ![Set diagnostics logs](media/active-directory-b2c-user-migration/pre-migration-error-message.png)

### <a name="step-46-optional-troubleshoot-your-rest-api"></a><span data-ttu-id="7f859-292">Step 4.6: (Optional) Troubleshoot your REST API</span><span class="sxs-lookup"><span data-stu-id="7f859-292">Step 4.6: (Optional) Troubleshoot your REST API</span></span>
<span data-ttu-id="7f859-293">You can view and monitor logging information in near-real time.</span><span class="sxs-lookup"><span data-stu-id="7f859-293">You can view and monitor logging information in near-real time.</span></span>

1. <span data-ttu-id="7f859-294">On your RESTful application's settings menu, under **Monitoring**, select **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="7f859-294">On your RESTful application's settings menu, under **Monitoring**, select **Diagnostic logs**.</span></span>

2. <span data-ttu-id="7f859-295">Set **Application Logging (Filesystem)** to **On**.</span><span class="sxs-lookup"><span data-stu-id="7f859-295">Set **Application Logging (Filesystem)** to **On**.</span></span>

3. <span data-ttu-id="7f859-296">Set the **Level** to **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="7f859-296">Set the **Level** to **Verbose**.</span></span>

4. <span data-ttu-id="7f859-297">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="7f859-297">Select **Save**</span></span>

    ![Set diagnostics logs](media/active-directory-b2c-user-migration/pre-migration-diagnostic-logs.png)

5. <span data-ttu-id="7f859-299">On the **Settings** menu, select **Log stream**.</span><span class="sxs-lookup"><span data-stu-id="7f859-299">On the **Settings** menu, select **Log stream**.</span></span>

6. <span data-ttu-id="7f859-300">Check the output of the RESTful API.</span><span class="sxs-lookup"><span data-stu-id="7f859-300">Check the output of the RESTful API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f859-301">Use the diagnostics logs only during development and testing.</span><span class="sxs-lookup"><span data-stu-id="7f859-301">Use the diagnostics logs only during development and testing.</span></span> <span data-ttu-id="7f859-302">The RESTful API output might contain confidential information that should not be exposed in production.</span><span class="sxs-lookup"><span data-stu-id="7f859-302">The RESTful API output might contain confidential information that should not be exposed in production.</span></span>
>

## <a name="optional-download-the-complete-policy-files"></a><span data-ttu-id="7f859-303">(Optional) Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="7f859-303">(Optional) Download the complete policy files</span></span>
<span data-ttu-id="7f859-304">After you complete the [Get started with custom policies][B2C-GetStartedCustom] walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="7f859-304">After you complete the [Get started with custom policies][B2C-GetStartedCustom] walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="7f859-305">For your reference, we have provided [Sample policy files][UserMigrationSample].</span><span class="sxs-lookup"><span data-stu-id="7f859-305">For your reference, we have provided [Sample policy files][UserMigrationSample].</span></span>

[AD-PasswordPolicies]: https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy
[AD-Powershell]: https://docs.microsoft.com/powershell/azure/active-directory/install-adv2
[AppService-Deploy]: https://docs.microsoft.com/aspnet/core/tutorials/publish-to-azure-webapp-using-vs
[B2C-AppRegister]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration
[B2C-GetStarted]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-get-started
[B2C-GetStartedCustom]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-get-started-custom
[B2C-GraphQuickStart]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet
[B2C-NavContext]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-navigate-to-b2c-context
[Portal]: https://portal.azure.com/
[UserMigrationSample]: https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-user-migration