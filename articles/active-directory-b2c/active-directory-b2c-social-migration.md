---
title: Migrate users with social identities in Azure Active Directory B2C | Microsoft Docs
description: Discuss core concepts on the migration of users with social identities into Azure AD B2C using Graph API.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 03/03/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: b9378face28b4d053dcd5f01b8f87126457cf339
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969059"
---
# <a name="azure-active-directory-b2c-migrate-users-with-social-identities"></a><span data-ttu-id="d617b-103">Azure Active Directory B2C: Migrate users with social identities</span><span class="sxs-lookup"><span data-stu-id="d617b-103">Azure Active Directory B2C: Migrate users with social identities</span></span>
<span data-ttu-id="d617b-104">When you plan to migrate your identity provider to Azure AD B2C, you may also need to migrate users with social identities.</span><span class="sxs-lookup"><span data-stu-id="d617b-104">When you plan to migrate your identity provider to Azure AD B2C, you may also need to migrate users with social identities.</span></span> <span data-ttu-id="d617b-105">This article explains how to migrate existing social identities accounts, such as: Facebook, LinkedIn, Microsoft, and Google accounts to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d617b-105">This article explains how to migrate existing social identities accounts, such as: Facebook, LinkedIn, Microsoft, and Google accounts to Azure AD B2C.</span></span> <span data-ttu-id="d617b-106">This article also applies to federated identities, however these migrations are less common.</span><span class="sxs-lookup"><span data-stu-id="d617b-106">This article also applies to federated identities, however these migrations are less common.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d617b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d617b-107">Prerequisites</span></span>
<span data-ttu-id="d617b-108">This article is a continuation of the user migration article, and focuses on social identity migration.</span><span class="sxs-lookup"><span data-stu-id="d617b-108">This article is a continuation of the user migration article, and focuses on social identity migration.</span></span> <span data-ttu-id="d617b-109">Before you start, read [user migration](active-directory-b2c-user-migration.md).</span><span class="sxs-lookup"><span data-stu-id="d617b-109">Before you start, read [user migration](active-directory-b2c-user-migration.md).</span></span>

## <a name="social-identities-migration-introduction"></a><span data-ttu-id="d617b-110">Social identities migration introduction</span><span class="sxs-lookup"><span data-stu-id="d617b-110">Social identities migration introduction</span></span>

* <span data-ttu-id="d617b-111">In Azure AD B2C, **local accounts** sign-in names (user name or email address) are stored in the `signInNames` collection in the user record.</span><span class="sxs-lookup"><span data-stu-id="d617b-111">In Azure AD B2C, **local accounts** sign-in names (user name or email address) are stored in the `signInNames` collection in the user record.</span></span> <span data-ttu-id="d617b-112">The `signInNames` contains one or more `signInName` records that specify the sign-in names for the user.</span><span class="sxs-lookup"><span data-stu-id="d617b-112">The `signInNames` contains one or more `signInName` records that specify the sign-in names for the user.</span></span> <span data-ttu-id="d617b-113">Each sign-in name must be unique across the tenant.</span><span class="sxs-lookup"><span data-stu-id="d617b-113">Each sign-in name must be unique across the tenant.</span></span>

* <span data-ttu-id="d617b-114">**Social accounts'** identities are stored in `userIdentities` collection.</span><span class="sxs-lookup"><span data-stu-id="d617b-114">**Social accounts'** identities are stored in `userIdentities` collection.</span></span> <span data-ttu-id="d617b-115">The entry specifies the `issuer` (identity provider name) such as facebook.com and the `issuerUserId`, which is a unique user identifier for the issuer.</span><span class="sxs-lookup"><span data-stu-id="d617b-115">The entry specifies the `issuer` (identity provider name) such as facebook.com and the `issuerUserId`, which is a unique user identifier for the issuer.</span></span> <span data-ttu-id="d617b-116">The `userIdentities` attribute contains one or more UserIdentity records that specify the social account type and the unique user identifier from the social identity provider.</span><span class="sxs-lookup"><span data-stu-id="d617b-116">The `userIdentities` attribute contains one or more UserIdentity records that specify the social account type and the unique user identifier from the social identity provider.</span></span>

* <span data-ttu-id="d617b-117">**Combine local account with social identity**.</span><span class="sxs-lookup"><span data-stu-id="d617b-117">**Combine local account with social identity**.</span></span> <span data-ttu-id="d617b-118">As mentioned, local account sign-in names, and social account identities are stored in different attributes.</span><span class="sxs-lookup"><span data-stu-id="d617b-118">As mentioned, local account sign-in names, and social account identities are stored in different attributes.</span></span> <span data-ttu-id="d617b-119">`signInNames` is used for local account, while `userIdentities` for social account.</span><span class="sxs-lookup"><span data-stu-id="d617b-119">`signInNames` is used for local account, while `userIdentities` for social account.</span></span> <span data-ttu-id="d617b-120">A single Azure AD B2C account, can be a local account only, social account only, or combine a local account with social identity in one user record.</span><span class="sxs-lookup"><span data-stu-id="d617b-120">A single Azure AD B2C account, can be a local account only, social account only, or combine a local account with social identity in one user record.</span></span> <span data-ttu-id="d617b-121">This behavior allows you to manage a single account, while a user can sign in with the local account credential(s) or with the social identities.</span><span class="sxs-lookup"><span data-stu-id="d617b-121">This behavior allows you to manage a single account, while a user can sign in with the local account credential(s) or with the social identities.</span></span>

* <span data-ttu-id="d617b-122">`UserIdentity` Type - Contains information about the identity of a social account user in an Azure AD B2C tenant:</span><span class="sxs-lookup"><span data-stu-id="d617b-122">`UserIdentity` Type - Contains information about the identity of a social account user in an Azure AD B2C tenant:</span></span>
    * <span data-ttu-id="d617b-123">`issuer` The string representation of the identity provider that issued the user identifier, such as facebook.com.</span><span class="sxs-lookup"><span data-stu-id="d617b-123">`issuer` The string representation of the identity provider that issued the user identifier, such as facebook.com.</span></span>
    * <span data-ttu-id="d617b-124">`issuerUserId` The unique user identifier used by the social identity provider in base64 format.</span><span class="sxs-lookup"><span data-stu-id="d617b-124">`issuerUserId` The unique user identifier used by the social identity provider in base64 format.</span></span>

    ```JSON
    "userIdentities": [{
            "issuer": "Facebook.com",
            "issuerUserId": "MTIzNDU2Nzg5MA=="
        }
    ]
    ```

* Depending on the identity provider, the **Social user ID** is a unique value for a given user per application or development account. Configure the Azure AD B2C policy with the same application ID that was previously assigned by the social provider. <span data-ttu-id="d617b-127">Or another application within the same development account.</span><span class="sxs-lookup"><span data-stu-id="d617b-127">Or another application within the same development account.</span></span>

## <a name="use-graph-api-to-migrate-users"></a><span data-ttu-id="d617b-128">Use Graph API to migrate users</span><span class="sxs-lookup"><span data-stu-id="d617b-128">Use Graph API to migrate users</span></span>
<span data-ttu-id="d617b-129">You create the Azure AD B2C user account via [Graph API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet).</span><span class="sxs-lookup"><span data-stu-id="d617b-129">You create the Azure AD B2C user account via [Graph API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet).</span></span> <span data-ttu-id="d617b-130">To communicate with the Graph API, you first must have a service account with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="d617b-130">To communicate with the Graph API, you first must have a service account with administrative privileges.</span></span> <span data-ttu-id="d617b-131">In Azure AD, you register an application and authentication to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d617b-131">In Azure AD, you register an application and authentication to Azure AD.</span></span> <span data-ttu-id="d617b-132">The application credentials are Application ID and Application Secret.</span><span class="sxs-lookup"><span data-stu-id="d617b-132">The application credentials are Application ID and Application Secret.</span></span> <span data-ttu-id="d617b-133">The application acts as itself, not as a user, to call the Graph API.</span><span class="sxs-lookup"><span data-stu-id="d617b-133">The application acts as itself, not as a user, to call the Graph API.</span></span> <span data-ttu-id="d617b-134">Follow the instructions in step 1 in [User migration](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-user-migration#step-1-use-graph-api-to-migrate-users) article.</span><span class="sxs-lookup"><span data-stu-id="d617b-134">Follow the instructions in step 1 in [User migration](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-user-migration#step-1-use-graph-api-to-migrate-users) article.</span></span>

## <a name="required-properties"></a><span data-ttu-id="d617b-135">Required properties</span><span class="sxs-lookup"><span data-stu-id="d617b-135">Required properties</span></span>
<span data-ttu-id="d617b-136">The following list shows the properties that are required when you create a user.</span><span class="sxs-lookup"><span data-stu-id="d617b-136">The following list shows the properties that are required when you create a user.</span></span>
* <span data-ttu-id="d617b-137">**accountEnabled** - true</span><span class="sxs-lookup"><span data-stu-id="d617b-137">**accountEnabled** - true</span></span>
* <span data-ttu-id="d617b-138">**displayName** - The name to display in the address book for the user.</span><span class="sxs-lookup"><span data-stu-id="d617b-138">**displayName** - The name to display in the address book for the user.</span></span>
* <span data-ttu-id="d617b-139">**passwordProfile** - The password profile for the user.</span><span class="sxs-lookup"><span data-stu-id="d617b-139">**passwordProfile** - The password profile for the user.</span></span> 

> [!NOTE]
> <span data-ttu-id="d617b-140">For social account only (without local account credentials), you still must specify the password.</span><span class="sxs-lookup"><span data-stu-id="d617b-140">For social account only (without local account credentials), you still must specify the password.</span></span> <span data-ttu-id="d617b-141">Azure AD B2C ignores the password you specify for social accounts.</span><span class="sxs-lookup"><span data-stu-id="d617b-141">Azure AD B2C ignores the password you specify for social accounts.</span></span>

* <span data-ttu-id="d617b-142">**userPrincipalName** - The user principal name (someuser@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="d617b-142">**userPrincipalName** - The user principal name (someuser@contoso.com).</span></span> <span data-ttu-id="d617b-143">The user principal name must contain one of the verified domains for the tenant.</span><span class="sxs-lookup"><span data-stu-id="d617b-143">The user principal name must contain one of the verified domains for the tenant.</span></span> <span data-ttu-id="d617b-144">To specify the UPN, generate new GUID value, concatenate with `@` and your tenant name.</span><span class="sxs-lookup"><span data-stu-id="d617b-144">To specify the UPN, generate new GUID value, concatenate with `@` and your tenant name.</span></span>
* <span data-ttu-id="d617b-145">**mailNickname** - The mail alias for the user.</span><span class="sxs-lookup"><span data-stu-id="d617b-145">**mailNickname** - The mail alias for the user.</span></span> <span data-ttu-id="d617b-146">This value can be the same ID that you use for the userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="d617b-146">This value can be the same ID that you use for the userPrincipalName.</span></span> 
* <span data-ttu-id="d617b-147">**signInNames** - One or more SignInName records that specify the sign-in names for the user.</span><span class="sxs-lookup"><span data-stu-id="d617b-147">**signInNames** - One or more SignInName records that specify the sign-in names for the user.</span></span> <span data-ttu-id="d617b-148">Each sign-in name must be unique across the company/tenant.</span><span class="sxs-lookup"><span data-stu-id="d617b-148">Each sign-in name must be unique across the company/tenant.</span></span> <span data-ttu-id="d617b-149">For social account only, this property can be left empty.</span><span class="sxs-lookup"><span data-stu-id="d617b-149">For social account only, this property can be left empty.</span></span>
* <span data-ttu-id="d617b-150">**userIdentities** - One or more UserIdentity records that specify the social account type and the unique user identifier from the social identity provider.</span><span class="sxs-lookup"><span data-stu-id="d617b-150">**userIdentities** - One or more UserIdentity records that specify the social account type and the unique user identifier from the social identity provider.</span></span>
* <span data-ttu-id="d617b-151">[optional] **otherMails** - For social account only, the user's email addresses</span><span class="sxs-lookup"><span data-stu-id="d617b-151">[optional] **otherMails** - For social account only, the user's email addresses</span></span> 

<span data-ttu-id="d617b-152">For more information, see: [Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)</span><span class="sxs-lookup"><span data-stu-id="d617b-152">For more information, see: [Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)</span></span>

## <a name="migrate-social-account-only"></a><span data-ttu-id="d617b-153">Migrate social account (only)</span><span class="sxs-lookup"><span data-stu-id="d617b-153">Migrate social account (only)</span></span>
<span data-ttu-id="d617b-154">To create social account only, without local account credentials.</span><span class="sxs-lookup"><span data-stu-id="d617b-154">To create social account only, without local account credentials.</span></span> <span data-ttu-id="d617b-155">Send HTTPS POST request to Graph API.</span><span class="sxs-lookup"><span data-stu-id="d617b-155">Send HTTPS POST request to Graph API.</span></span> <span data-ttu-id="d617b-156">The request body contains the properties of the social account user to create.</span><span class="sxs-lookup"><span data-stu-id="d617b-156">The request body contains the properties of the social account user to create.</span></span> <span data-ttu-id="d617b-157">At a minimum, you must specify the required properties.</span><span class="sxs-lookup"><span data-stu-id="d617b-157">At a minimum, you must specify the required properties.</span></span> 


<span data-ttu-id="d617b-158">**POST**  https://graph.windows.net/tenant-name.onmicrosoft.com/users</span><span class="sxs-lookup"><span data-stu-id="d617b-158">**POST**  https://graph.windows.net/tenant-name.onmicrosoft.com/users</span></span>

<span data-ttu-id="d617b-159">Submit the following form-data:</span><span class="sxs-lookup"><span data-stu-id="d617b-159">Submit the following form-data:</span></span> 

```JSON
{
    "objectId": null,
    "accountEnabled": true,
    "mailNickname": "c8c3d3b8-60cf-4c76-9aa7-eb3235b190c8",
    "signInNames": [],
    "creationType": null,
    "displayName": "Sara Bell",
    "givenName": "Sara",
    "surname": "Bell",
    "passwordProfile": {
        "password": "Test1234",
        "forceChangePasswordNextLogin": false
    },
    "passwordPolicies": null,
    "userIdentities": [{
            "issuer": "Facebook.com",
            "issuerUserId": "MTIzNDU2Nzg5MA=="
        }
    ],
    "otherMails": ["sara@live.com"],
    "userPrincipalName": "c8c3d3b8-60cf-4c76-9aa7-eb3235b190c8@tenant-name.onmicrosoft.com"
}
```
## <a name="migrate-social-account-with-local-account"></a><span data-ttu-id="d617b-160">Migrate social account with local account</span><span class="sxs-lookup"><span data-stu-id="d617b-160">Migrate social account with local account</span></span>
<span data-ttu-id="d617b-161">To create a combined local account with social identities.</span><span class="sxs-lookup"><span data-stu-id="d617b-161">To create a combined local account with social identities.</span></span> <span data-ttu-id="d617b-162">Send HTTPS POST request to Graph API.</span><span class="sxs-lookup"><span data-stu-id="d617b-162">Send HTTPS POST request to Graph API.</span></span> <span data-ttu-id="d617b-163">The request body contains the properties of the social account user to create.</span><span class="sxs-lookup"><span data-stu-id="d617b-163">The request body contains the properties of the social account user to create.</span></span> <span data-ttu-id="d617b-164">At a minimum, you must specify the required properties.</span><span class="sxs-lookup"><span data-stu-id="d617b-164">At a minimum, you must specify the required properties.</span></span> 

<span data-ttu-id="d617b-165">**POST**  https://graph.windows.net/tenant-name.onmicrosoft.com/users</span><span class="sxs-lookup"><span data-stu-id="d617b-165">**POST**  https://graph.windows.net/tenant-name.onmicrosoft.com/users</span></span>

<span data-ttu-id="d617b-166">Submit following form-data:</span><span class="sxs-lookup"><span data-stu-id="d617b-166">Submit following form-data:</span></span> 

```JSON
{
    "objectId": null,
    "accountEnabled": true,
    "mailNickname": "5164db16-3eee-4629-bfda-dcc3326790e9",
    "signInNames": [{
            "type": "emailAddress",
            "value": "david@contoso.com"
        }
    ],
    "creationType": "LocalAccount",
    "displayName": "David Hor",
    "givenName": "David",
    "surname": "Hor",
    "passwordProfile": {
        "password": "1234567",
        "forceChangePasswordNextLogin": false
    },
    "passwordPolicies": "DisablePasswordExpiration,DisableStrongPassword",
    "userIdentities": [{
            "issuer": "contoso.com",
            "issuerUserId": "ZGF2aWRAY29udG9zby5jb20="
        }
    ],
    "otherMails": [],
    "userPrincipalName": "5164db16-3eee-4629-bfda-dcc3326790e9@tenant-name.onmicrosoft.com"
}
```

## <a name="frequently-asked-questions"></a><span data-ttu-id="d617b-167">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="d617b-167">Frequently asked questions</span></span>
### <a name="how-can-i-know-the-issuer-name"></a><span data-ttu-id="d617b-168">How can I know the issuer name?</span><span class="sxs-lookup"><span data-stu-id="d617b-168">How can I know the issuer name?</span></span>
<span data-ttu-id="d617b-169">The issuer name, or the identity provider name, is configured in your policy.</span><span class="sxs-lookup"><span data-stu-id="d617b-169">The issuer name, or the identity provider name, is configured in your policy.</span></span> <span data-ttu-id="d617b-170">If you don't know the value to specify in `issuer`, follow this procedure:</span><span class="sxs-lookup"><span data-stu-id="d617b-170">If you don't know the value to specify in `issuer`, follow this procedure:</span></span>
1. <span data-ttu-id="d617b-171">Sign in with one of the social accounts</span><span class="sxs-lookup"><span data-stu-id="d617b-171">Sign in with one of the social accounts</span></span>
2. <span data-ttu-id="d617b-172">From the JWT token, copy the `sub` value.</span><span class="sxs-lookup"><span data-stu-id="d617b-172">From the JWT token, copy the `sub` value.</span></span> <span data-ttu-id="d617b-173">The `sub` usually contains the user's object ID in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d617b-173">The `sub` usually contains the user's object ID in Azure AD B2C.</span></span> <span data-ttu-id="d617b-174">Or from Azure portal, open the user's properties and copy the object ID.</span><span class="sxs-lookup"><span data-stu-id="d617b-174">Or from Azure portal, open the user's properties and copy the object ID.</span></span>
3. <span data-ttu-id="d617b-175">Open [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net)</span><span class="sxs-lookup"><span data-stu-id="d617b-175">Open [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net)</span></span>
4. <span data-ttu-id="d617b-176">Sign in with your administrator.</span><span class="sxs-lookup"><span data-stu-id="d617b-176">Sign in with your administrator.</span></span> <span data-ttu-id="d617b-177">N</span><span class="sxs-lookup"><span data-stu-id="d617b-177">N</span></span>
5. <span data-ttu-id="d617b-178">Run following GET request.</span><span class="sxs-lookup"><span data-stu-id="d617b-178">Run following GET request.</span></span> <span data-ttu-id="d617b-179">Replace the userObjectId with the user ID you copied.</span><span class="sxs-lookup"><span data-stu-id="d617b-179">Replace the userObjectId with the user ID you copied.</span></span> <span data-ttu-id="d617b-180">**GET** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span><span class="sxs-lookup"><span data-stu-id="d617b-180">**GET** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span></span>
6. <span data-ttu-id="d617b-181">Locate the `userIdentities` element inside the JSON return from Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d617b-181">Locate the `userIdentities` element inside the JSON return from Azure AD B2C.</span></span>
7. <span data-ttu-id="d617b-182">[Optional] You may also want to decode the `issuerUserId` value.</span><span class="sxs-lookup"><span data-stu-id="d617b-182">[Optional] You may also want to decode the `issuerUserId` value.</span></span>

> [!NOTE]
> <span data-ttu-id="d617b-183">Use a B2C tenant administrator account that is local to the B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="d617b-183">Use a B2C tenant administrator account that is local to the B2C tenant.</span></span> <span data-ttu-id="d617b-184">The account name syntax is admin@tenant-name.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d617b-184">The account name syntax is admin@tenant-name.onmicrosoft.com.</span></span>

### <a name="is-it-possible-to-add-social-identity-to-an-existing-local-account"></a><span data-ttu-id="d617b-185">Is it possible to add social identity to an existing local account?</span><span class="sxs-lookup"><span data-stu-id="d617b-185">Is it possible to add social identity to an existing local account?</span></span>
<span data-ttu-id="d617b-186">Yes.</span><span class="sxs-lookup"><span data-stu-id="d617b-186">Yes.</span></span> <span data-ttu-id="d617b-187">You can add the social identity after the local account has been created.</span><span class="sxs-lookup"><span data-stu-id="d617b-187">You can add the social identity after the local account has been created.</span></span> <span data-ttu-id="d617b-188">Run HTTPS PATCH request.</span><span class="sxs-lookup"><span data-stu-id="d617b-188">Run HTTPS PATCH request.</span></span> <span data-ttu-id="d617b-189">Replace the userObjectId with the user ID you want to update.</span><span class="sxs-lookup"><span data-stu-id="d617b-189">Replace the userObjectId with the user ID you want to update.</span></span> 

<span data-ttu-id="d617b-190">**PATCH** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span><span class="sxs-lookup"><span data-stu-id="d617b-190">**PATCH** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span></span>

<span data-ttu-id="d617b-191">Submit following form-data:</span><span class="sxs-lookup"><span data-stu-id="d617b-191">Submit following form-data:</span></span> 

```JSON
{
    "userIdentities": [
        {
            "issuer": "Facebook.com",
            "issuerUserId": "MTIzNDU2Nzg5MA=="
        }
    ]
}
```

### <a name="is-it-possible-to-add-multiple-social-identities"></a><span data-ttu-id="d617b-192">Is it possible to add multiple social identities?</span><span class="sxs-lookup"><span data-stu-id="d617b-192">Is it possible to add multiple social identities?</span></span>
<span data-ttu-id="d617b-193">Yes.</span><span class="sxs-lookup"><span data-stu-id="d617b-193">Yes.</span></span> <span data-ttu-id="d617b-194">You can add multiple social identities for a single Azure AD B2C account.</span><span class="sxs-lookup"><span data-stu-id="d617b-194">You can add multiple social identities for a single Azure AD B2C account.</span></span> <span data-ttu-id="d617b-195">Run HTTPS PATCH request.</span><span class="sxs-lookup"><span data-stu-id="d617b-195">Run HTTPS PATCH request.</span></span> <span data-ttu-id="d617b-196">Replace the userObjectId with the user ID.</span><span class="sxs-lookup"><span data-stu-id="d617b-196">Replace the userObjectId with the user ID.</span></span> 

<span data-ttu-id="d617b-197">**PATCH** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span><span class="sxs-lookup"><span data-stu-id="d617b-197">**PATCH** https://graph.windows.net/tenant-name.onmicrosoft.com/users/userObjectId</span></span>

<span data-ttu-id="d617b-198">Submit following form-data:</span><span class="sxs-lookup"><span data-stu-id="d617b-198">Submit following form-data:</span></span> 

```JSON
{
    "userIdentities": [
        {
            "issuer": "google.com",
            "issuerUserId": "MjQzMjE2NTc4NTQ="
        },
        {
            "issuer": "facebook.com",
            "issuerUserId": "MTIzNDU2Nzg5MA=="
        }
    ]
}
```

## <a name="optional-user-migration-application-sample"></a><span data-ttu-id="d617b-199">[Optional] User migration application sample</span><span class="sxs-lookup"><span data-stu-id="d617b-199">[Optional] User migration application sample</span></span>
<span data-ttu-id="d617b-200">[Download and run the sample app V2](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-user-migration).</span><span class="sxs-lookup"><span data-stu-id="d617b-200">[Download and run the sample app V2](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-user-migration).</span></span> <span data-ttu-id="d617b-201">The sample app V2 uses a JSON file that contains dummy user data, including: local account, social account, and local & social identities in single account.</span><span class="sxs-lookup"><span data-stu-id="d617b-201">The sample app V2 uses a JSON file that contains dummy user data, including: local account, social account, and local & social identities in single account.</span></span>  <span data-ttu-id="d617b-202">To edit the JSON file, open the `AADB2C.UserMigration.sln` Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="d617b-202">To edit the JSON file, open the `AADB2C.UserMigration.sln` Visual Studio solution.</span></span> <span data-ttu-id="d617b-203">In the `AADB2C.UserMigration` project, open the `UsersData.json` file.</span><span class="sxs-lookup"><span data-stu-id="d617b-203">In the `AADB2C.UserMigration` project, open the `UsersData.json` file.</span></span> <span data-ttu-id="d617b-204">The file contains a list of user entities.</span><span class="sxs-lookup"><span data-stu-id="d617b-204">The file contains a list of user entities.</span></span> <span data-ttu-id="d617b-205">Each user entity has the following properties:</span><span class="sxs-lookup"><span data-stu-id="d617b-205">Each user entity has the following properties:</span></span>
* <span data-ttu-id="d617b-206">**signInName** - For local account, e-mail address to sign-in</span><span class="sxs-lookup"><span data-stu-id="d617b-206">**signInName** - For local account, e-mail address to sign-in</span></span>
* <span data-ttu-id="d617b-207">**displayName** - User's display name</span><span class="sxs-lookup"><span data-stu-id="d617b-207">**displayName** - User's display name</span></span>
* <span data-ttu-id="d617b-208">**firstName** - User's first name</span><span class="sxs-lookup"><span data-stu-id="d617b-208">**firstName** - User's first name</span></span>
* <span data-ttu-id="d617b-209">**lastName** - User's last name</span><span class="sxs-lookup"><span data-stu-id="d617b-209">**lastName** - User's last name</span></span>
* <span data-ttu-id="d617b-210">**password** For local account, user's password (can be empty)</span><span class="sxs-lookup"><span data-stu-id="d617b-210">**password** For local account, user's password (can be empty)</span></span>
* <span data-ttu-id="d617b-211">**issuer** - For social account, the identity provider name</span><span class="sxs-lookup"><span data-stu-id="d617b-211">**issuer** - For social account, the identity provider name</span></span>
* <span data-ttu-id="d617b-212">**issuerUserId** - For social account, the unique user identifier used by the social identity provider.</span><span class="sxs-lookup"><span data-stu-id="d617b-212">**issuerUserId** - For social account, the unique user identifier used by the social identity provider.</span></span> <span data-ttu-id="d617b-213">The value should be in clear text.</span><span class="sxs-lookup"><span data-stu-id="d617b-213">The value should be in clear text.</span></span> <span data-ttu-id="d617b-214">The sample app encodes this value to  base64.</span><span class="sxs-lookup"><span data-stu-id="d617b-214">The sample app encodes this value to  base64.</span></span>
* <span data-ttu-id="d617b-215">**email** For social account only (not combined), user's email address</span><span class="sxs-lookup"><span data-stu-id="d617b-215">**email** For social account only (not combined), user's email address</span></span>

```JSON
{
  "userType": "emailAddress",
  "Users": [
    {
      // Local account only
      "signInName": "James@contoso.com",
      "displayName": "James Martin",
      "firstName": "James",
      "lastName": "Martin",
      "password": "Pass!w0rd"
    },
    {
      // Social account only
      "issuer": "Facebook.com",
      "issuerUserId": "1234567890",
      "email": "sara@contoso.com",
      "displayName": "Sara Bell",
      "firstName": "Sara",
      "lastName": "Bell"
    },
    {
      // Combine local account with social identity
      "signInName": "david@contoso.com",
      "issuer": "Facebook.com",
      "issuerUserId": "0987654321",
      "displayName": "David Hor",
      "firstName": "David",
      "lastName": "Hor",
      "password": "Pass!w0rd"
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="d617b-216">If you don't update the UsersData.json file in the sample with your data, you can sign-in with the sample local account credentials but not with the social account examples.</span><span class="sxs-lookup"><span data-stu-id="d617b-216">If you don't update the UsersData.json file in the sample with your data, you can sign-in with the sample local account credentials but not with the social account examples.</span></span> <span data-ttu-id="d617b-217">To migrate your social accounts, provide real data.</span><span class="sxs-lookup"><span data-stu-id="d617b-217">To migrate your social accounts, provide real data.</span></span>

<span data-ttu-id="d617b-218">For more information, how to use the sample app, see [Azure Active Directory B2C: User migration](active-directory-b2c-user-migration.md)</span><span class="sxs-lookup"><span data-stu-id="d617b-218">For more information, how to use the sample app, see [Azure Active Directory B2C: User migration](active-directory-b2c-user-migration.md)</span></span>
