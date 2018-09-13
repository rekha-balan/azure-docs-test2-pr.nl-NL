---
title: Configure the role claim issued in the SAML token for enterprise applications in Azure Active Directory | Microsoft Docs
description: Learn how to configure the role claim issued in the SAML token for enterprise applications in Azure Active Directory
services: active-directory
documentationcenter: ''
author: jeevansd
manager: mtillman
editor: ''
ms.assetid: eb2b3741-3cde-45c8-b639-a636f3df3b74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2018
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: cb4c9f91c7a116e6171a8e94030b6bb40fdb38ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868381"
---
# <a name="configure-the-role-claim-issued-in-the-saml-token-for-enterprise-applications-in-azure-active-directory"></a><span data-ttu-id="41f28-103">Configure the role claim issued in the SAML token for enterprise applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41f28-103">Configure the role claim issued in the SAML token for enterprise applications in Azure Active Directory</span></span>

<span data-ttu-id="41f28-104">By using Azure Active Directory (Azure AD), you can customize the claim type for the role claim in the response token that you receive after you authorize an app.</span><span class="sxs-lookup"><span data-stu-id="41f28-104">By using Azure Active Directory (Azure AD), you can customize the claim type for the role claim in the response token that you receive after you authorize an app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41f28-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41f28-105">Prerequisites</span></span>
- <span data-ttu-id="41f28-106">An Azure AD subscription with directory setup.</span><span class="sxs-lookup"><span data-stu-id="41f28-106">An Azure AD subscription with directory setup.</span></span>
- <span data-ttu-id="41f28-107">A subscription that has single sign-on (SSO) enabled.</span><span class="sxs-lookup"><span data-stu-id="41f28-107">A subscription that has single sign-on (SSO) enabled.</span></span> <span data-ttu-id="41f28-108">You must configure SSO with your application.</span><span class="sxs-lookup"><span data-stu-id="41f28-108">You must configure SSO with your application.</span></span>

## <a name="when-to-use-this-feature"></a><span data-ttu-id="41f28-109">When to use this feature</span><span class="sxs-lookup"><span data-stu-id="41f28-109">When to use this feature</span></span>

<span data-ttu-id="41f28-110">If your application expects custom roles to be passed in a SAML response, you need to use this feature.</span><span class="sxs-lookup"><span data-stu-id="41f28-110">If your application expects custom roles to be passed in a SAML response, you need to use this feature.</span></span> <span data-ttu-id="41f28-111">You can create as many roles as you need to be passed back from Azure AD to your application.</span><span class="sxs-lookup"><span data-stu-id="41f28-111">You can create as many roles as you need to be passed back from Azure AD to your application.</span></span>

## <a name="create-roles-for-an-application"></a><span data-ttu-id="41f28-112">Create roles for an application</span><span class="sxs-lookup"><span data-stu-id="41f28-112">Create roles for an application</span></span>

1. <span data-ttu-id="41f28-113">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="41f28-113">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory icon][1]

2. <span data-ttu-id="41f28-115">Select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="41f28-115">Select **Enterprise applications**.</span></span> <span data-ttu-id="41f28-116">Then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="41f28-116">Then select **All applications**.</span></span>

    ![Enterprise applications pane][2]

3. <span data-ttu-id="41f28-118">To add a new application, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="41f28-118">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    !["New application" button][3]

4. <span data-ttu-id="41f28-120">In the search box, type the name of your application, and then select your application from the result panel.</span><span class="sxs-lookup"><span data-stu-id="41f28-120">In the search box, type the name of your application, and then select your application from the result panel.</span></span> <span data-ttu-id="41f28-121">Select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="41f28-121">Select the **Add** button to add the application.</span></span>

    ![Application in the results list](./media/active-directory-enterprise-app-role-management/tutorial_app_addfromgallery.png)

5. <span data-ttu-id="41f28-123">After the application is added, go to the **Properties** page and copy the object ID.</span><span class="sxs-lookup"><span data-stu-id="41f28-123">After the application is added, go to the **Properties** page and copy the object ID.</span></span>

    ![Properties Page](./media/active-directory-enterprise-app-role-management/tutorial_app_properties.png)

6. <span data-ttu-id="41f28-125">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window and take the following steps:</span><span class="sxs-lookup"><span data-stu-id="41f28-125">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window and take the following steps:</span></span>

    <span data-ttu-id="41f28-126">a.</span><span class="sxs-lookup"><span data-stu-id="41f28-126">a.</span></span> <span data-ttu-id="41f28-127">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="41f28-127">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span></span>

    <span data-ttu-id="41f28-128">b.</span><span class="sxs-lookup"><span data-stu-id="41f28-128">b.</span></span> <span data-ttu-id="41f28-129">You need sufficient permissions to create the roles.</span><span class="sxs-lookup"><span data-stu-id="41f28-129">You need sufficient permissions to create the roles.</span></span> <span data-ttu-id="41f28-130">Select **modify permissions** to get the permissions.</span><span class="sxs-lookup"><span data-stu-id="41f28-130">Select **modify permissions** to get the permissions.</span></span>

      ![The "modify permissions" button](./media/active-directory-enterprise-app-role-management/graph-explorer-new9.png)

    <span data-ttu-id="41f28-132">c.</span><span class="sxs-lookup"><span data-stu-id="41f28-132">c.</span></span> <span data-ttu-id="41f28-133">Select the following permissions from the list (if you don't have these already) and select **Modify Permissions**.</span><span class="sxs-lookup"><span data-stu-id="41f28-133">Select the following permissions from the list (if you don't have these already) and select **Modify Permissions**.</span></span>

      ![List of permissions and "Modify Permissions" button](./media/active-directory-enterprise-app-role-management/graph-explorer-new10.png)

    > [!Note]
    > <span data-ttu-id="41f28-135">Cloud App Administrator and App Administrator role will not work in this scenario as we need the Global Admin permissions for Directory Read and Write.</span><span class="sxs-lookup"><span data-stu-id="41f28-135">Cloud App Administrator and App Administrator role will not work in this scenario as we need the Global Admin permissions for Directory Read and Write.</span></span>

    <span data-ttu-id="41f28-136">d.</span><span class="sxs-lookup"><span data-stu-id="41f28-136">d.</span></span> <span data-ttu-id="41f28-137">Accept the consent.</span><span class="sxs-lookup"><span data-stu-id="41f28-137">Accept the consent.</span></span> <span data-ttu-id="41f28-138">You're logged in to the system again.</span><span class="sxs-lookup"><span data-stu-id="41f28-138">You're logged in to the system again.</span></span>

    <span data-ttu-id="41f28-139">e.</span><span class="sxs-lookup"><span data-stu-id="41f28-139">e.</span></span> <span data-ttu-id="41f28-140">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span><span class="sxs-lookup"><span data-stu-id="41f28-140">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span></span>

     `https://graph.microsoft.com/beta/servicePrincipals`

      <span data-ttu-id="41f28-141">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span><span class="sxs-lookup"><span data-stu-id="41f28-141">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span></span>

      ![Graph Explorer dialog box, with the query for fetching service principals](./media/active-directory-enterprise-app-role-management/graph-explorer-new1.png)

      > [!Note]
      > <span data-ttu-id="41f28-143">We are already in the process of upgrading the APIs so customers might see some disruption in the service.</span><span class="sxs-lookup"><span data-stu-id="41f28-143">We are already in the process of upgrading the APIs so customers might see some disruption in the service.</span></span>

    <span data-ttu-id="41f28-144">f.</span><span class="sxs-lookup"><span data-stu-id="41f28-144">f.</span></span> <span data-ttu-id="41f28-145">From the list of fetched service principals, get the one that you need to modify.</span><span class="sxs-lookup"><span data-stu-id="41f28-145">From the list of fetched service principals, get the one that you need to modify.</span></span> <span data-ttu-id="41f28-146">You can also use Ctrl+F to search the application from all the listed service principals.</span><span class="sxs-lookup"><span data-stu-id="41f28-146">You can also use Ctrl+F to search the application from all the listed service principals.</span></span> <span data-ttu-id="41f28-147">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span><span class="sxs-lookup"><span data-stu-id="41f28-147">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span></span>

      `https://graph.microsoft.com/beta/servicePrincipals/<objectID>`

      ![Query for getting the service principal that you need to modify](./media/active-directory-enterprise-app-role-management/graph-explorer-new2.png)

    <span data-ttu-id="41f28-149">g.</span><span class="sxs-lookup"><span data-stu-id="41f28-149">g.</span></span> <span data-ttu-id="41f28-150">Extract the **appRoles** property from the service principal object.</span><span class="sxs-lookup"><span data-stu-id="41f28-150">Extract the **appRoles** property from the service principal object.</span></span>

      ![Details of the appRoles property](./media/active-directory-enterprise-app-role-management/graph-explorer-new3.png)

      > [!Note]
      > <span data-ttu-id="41f28-152">If you're using the custom app (not the Azure Marketplace app), you see two default roles: user and msiam_access.</span><span class="sxs-lookup"><span data-stu-id="41f28-152">If you're using the custom app (not the Azure Marketplace app), you see two default roles: user and msiam_access.</span></span> <span data-ttu-id="41f28-153">For the Marketplace app, msiam_access is the only default role.</span><span class="sxs-lookup"><span data-stu-id="41f28-153">For the Marketplace app, msiam_access is the only default role.</span></span> <span data-ttu-id="41f28-154">You don't need to make any changes in the default roles.</span><span class="sxs-lookup"><span data-stu-id="41f28-154">You don't need to make any changes in the default roles.</span></span>

    <span data-ttu-id="41f28-155">h.</span><span class="sxs-lookup"><span data-stu-id="41f28-155">h.</span></span> <span data-ttu-id="41f28-156">Generate new roles for your application.</span><span class="sxs-lookup"><span data-stu-id="41f28-156">Generate new roles for your application.</span></span>

      <span data-ttu-id="41f28-157">The following JSON is an example of the **appRoles** object.</span><span class="sxs-lookup"><span data-stu-id="41f28-157">The following JSON is an example of the **appRoles** object.</span></span> <span data-ttu-id="41f28-158">Create a similar object to add the roles that you want for your application.</span><span class="sxs-lookup"><span data-stu-id="41f28-158">Create a similar object to add the roles that you want for your application.</span></span>

      ```
      {
         "appRoles": [
          {
              "allowedMemberTypes": [
                  "User"
              ],
              "description": "msiam_access",
              "displayName": "msiam_access",
              "id": "b9632174-c057-4f7e-951b-be3adc52bfe6",
              "isEnabled": true,
              "origin": "Application",
              "value": null
          },
          {
              "allowedMemberTypes": [
                  "User"
              ],
              "description": "Administrators Only",
              "displayName": "Admin",
              "id": "4f8f8640-f081-492d-97a0-caf24e9bc134",
              "isEnabled": true,
              "origin": "ServicePrincipal",
              "value": "Administrator"
          }
      ]
      }
      ```

      > [!Note]
      > <span data-ttu-id="41f28-159">You can only add new roles after msiam_access for the patch operation.</span><span class="sxs-lookup"><span data-stu-id="41f28-159">You can only add new roles after msiam_access for the patch operation.</span></span> <span data-ttu-id="41f28-160">Also, you can add as many roles as your organization needs.</span><span class="sxs-lookup"><span data-stu-id="41f28-160">Also, you can add as many roles as your organization needs.</span></span> <span data-ttu-id="41f28-161">Azure AD will send the value of these roles as the claim value in the SAML response.</span><span class="sxs-lookup"><span data-stu-id="41f28-161">Azure AD will send the value of these roles as the claim value in the SAML response.</span></span> <span data-ttu-id="41f28-162">To generate the GUID values for the ID of new roles use the web tools like [this](https://www.guidgenerator.com/)</span><span class="sxs-lookup"><span data-stu-id="41f28-162">To generate the GUID values for the ID of new roles use the web tools like [this](https://www.guidgenerator.com/)</span></span>

    <span data-ttu-id="41f28-163">i.</span><span class="sxs-lookup"><span data-stu-id="41f28-163">i.</span></span> <span data-ttu-id="41f28-164">Go back to Graph Explorer and change the method from **GET** to **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="41f28-164">Go back to Graph Explorer and change the method from **GET** to **PATCH**.</span></span> <span data-ttu-id="41f28-165">Patch the service principal object to have the desired roles by updating the **appRoles** property like the one shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="41f28-165">Patch the service principal object to have the desired roles by updating the **appRoles** property like the one shown in the preceding example.</span></span> <span data-ttu-id="41f28-166">Select **Run Query** to execute the patch operation.</span><span class="sxs-lookup"><span data-stu-id="41f28-166">Select **Run Query** to execute the patch operation.</span></span> <span data-ttu-id="41f28-167">A success message confirms the creation of the role.</span><span class="sxs-lookup"><span data-stu-id="41f28-167">A success message confirms the creation of the role.</span></span>

      ![Patch operation with success message](./media/active-directory-enterprise-app-role-management/graph-explorer-new11.png)

7. <span data-ttu-id="41f28-169">After the service principal is patched with more roles, you can assign users to the respective roles.</span><span class="sxs-lookup"><span data-stu-id="41f28-169">After the service principal is patched with more roles, you can assign users to the respective roles.</span></span> <span data-ttu-id="41f28-170">You can assign the users by going to portal and browsing to the application.</span><span class="sxs-lookup"><span data-stu-id="41f28-170">You can assign the users by going to portal and browsing to the application.</span></span> <span data-ttu-id="41f28-171">Select the **Users and groups** tab. This tab lists all the users and groups that are already assigned to the app.</span><span class="sxs-lookup"><span data-stu-id="41f28-171">Select the **Users and groups** tab. This tab lists all the users and groups that are already assigned to the app.</span></span> <span data-ttu-id="41f28-172">You can add new users on the new roles.</span><span class="sxs-lookup"><span data-stu-id="41f28-172">You can add new users on the new roles.</span></span> <span data-ttu-id="41f28-173">You can also select an existing user and select **Edit** to change the role.</span><span class="sxs-lookup"><span data-stu-id="41f28-173">You can also select an existing user and select **Edit** to change the role.</span></span>

    !["Users and groups" tab](./media/active-directory-enterprise-app-role-management/graph-explorer-new5.png)

    <span data-ttu-id="41f28-175">To assign the role to any user, select the new role and select the **Assign** button on the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="41f28-175">To assign the role to any user, select the new role and select the **Assign** button on the bottom of the page.</span></span>

    !["Edit Assignment" pane and "Select Role" pane](./media/active-directory-enterprise-app-role-management/graph-explorer-new6.png)

    > [!Note]
    > <span data-ttu-id="41f28-177">You need to refresh your session in the Azure portal to see new roles.</span><span class="sxs-lookup"><span data-stu-id="41f28-177">You need to refresh your session in the Azure portal to see new roles.</span></span>

8. <span data-ttu-id="41f28-178">Update the **Attributes** table to define a customized mapping of the role claim.</span><span class="sxs-lookup"><span data-stu-id="41f28-178">Update the **Attributes** table to define a customized mapping of the role claim.</span></span>

9. <span data-ttu-id="41f28-179">In the **User Attributes** section of the **Single sign-on** dialog box, configure the SAML token attribute as shown in the image and perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="41f28-179">In the **User Attributes** section of the **Single sign-on** dialog box, configure the SAML token attribute as shown in the image and perform the following steps.</span></span>

    | <span data-ttu-id="41f28-180">Attribute name</span><span class="sxs-lookup"><span data-stu-id="41f28-180">Attribute name</span></span> | <span data-ttu-id="41f28-181">Attribute value</span><span class="sxs-lookup"><span data-stu-id="41f28-181">Attribute value</span></span> |
    | -------------- | ----------------|
    | <span data-ttu-id="41f28-182">Role name</span><span class="sxs-lookup"><span data-stu-id="41f28-182">Role name</span></span>  | <span data-ttu-id="41f28-183">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="41f28-183">user.assignedroles</span></span> |

    <span data-ttu-id="41f28-184">a.</span><span class="sxs-lookup"><span data-stu-id="41f28-184">a.</span></span> <span data-ttu-id="41f28-185">Select **Add attribute** to open the **Add Attribute** pane.</span><span class="sxs-lookup"><span data-stu-id="41f28-185">Select **Add attribute** to open the **Add Attribute** pane.</span></span>

      !["Add attribute" button](./media/active-directory-enterprise-app-role-management/tutorial_attribute_04.png)

      !["Add Attribute" pane](./media/active-directory-enterprise-app-role-management/tutorial_attribute_05.png)

    <span data-ttu-id="41f28-188">b.</span><span class="sxs-lookup"><span data-stu-id="41f28-188">b.</span></span> <span data-ttu-id="41f28-189">In the **Name** box, type the attribute name as needed.</span><span class="sxs-lookup"><span data-stu-id="41f28-189">In the **Name** box, type the attribute name as needed.</span></span> <span data-ttu-id="41f28-190">This example uses **Role Name** as the claim name.</span><span class="sxs-lookup"><span data-stu-id="41f28-190">This example uses **Role Name** as the claim name.</span></span>

    <span data-ttu-id="41f28-191">c.</span><span class="sxs-lookup"><span data-stu-id="41f28-191">c.</span></span> <span data-ttu-id="41f28-192">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="41f28-192">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="41f28-193">d.</span><span class="sxs-lookup"><span data-stu-id="41f28-193">d.</span></span> <span data-ttu-id="41f28-194">Leave the **Namespace** box blank.</span><span class="sxs-lookup"><span data-stu-id="41f28-194">Leave the **Namespace** box blank.</span></span>

    <span data-ttu-id="41f28-195">e.</span><span class="sxs-lookup"><span data-stu-id="41f28-195">e.</span></span> <span data-ttu-id="41f28-196">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="41f28-196">Select **Ok**.</span></span>

10. <span data-ttu-id="41f28-197">To test your application in a single sign-on that's initiated by an identity provider, sign in to the [Access Panel](https://myapps.microsoft.com) and select your application tile.</span><span class="sxs-lookup"><span data-stu-id="41f28-197">To test your application in a single sign-on that's initiated by an identity provider, sign in to the [Access Panel](https://myapps.microsoft.com) and select your application tile.</span></span> <span data-ttu-id="41f28-198">In the SAML token, you should see all the assigned roles for the user with the claim name that you have given.</span><span class="sxs-lookup"><span data-stu-id="41f28-198">In the SAML token, you should see all the assigned roles for the user with the claim name that you have given.</span></span>

## <a name="update-an-existing-role"></a><span data-ttu-id="41f28-199">Update an existing role</span><span class="sxs-lookup"><span data-stu-id="41f28-199">Update an existing role</span></span>

<span data-ttu-id="41f28-200">To update an existing role, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="41f28-200">To update an existing role, perform the following steps:</span></span>

1. <span data-ttu-id="41f28-201">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).</span><span class="sxs-lookup"><span data-stu-id="41f28-201">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).</span></span>

2. <span data-ttu-id="41f28-202">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="41f28-202">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span></span>

3. <span data-ttu-id="41f28-203">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span><span class="sxs-lookup"><span data-stu-id="41f28-203">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span></span>

    `https://graph.microsoft.com/beta/servicePrincipals`

    <span data-ttu-id="41f28-204">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span><span class="sxs-lookup"><span data-stu-id="41f28-204">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span></span>

    ![Graph Explorer dialog box, with the query for fetching service principals](./media/active-directory-enterprise-app-role-management/graph-explorer-new1.png)

4. <span data-ttu-id="41f28-206">From the list of fetched service principals, get the one that you need to modify.</span><span class="sxs-lookup"><span data-stu-id="41f28-206">From the list of fetched service principals, get the one that you need to modify.</span></span> <span data-ttu-id="41f28-207">You can also use Ctrl+F to search the application from all the listed service principals.</span><span class="sxs-lookup"><span data-stu-id="41f28-207">You can also use Ctrl+F to search the application from all the listed service principals.</span></span> <span data-ttu-id="41f28-208">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span><span class="sxs-lookup"><span data-stu-id="41f28-208">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span></span>

    `https://graph.microsoft.com/beta/servicePrincipals/<objectID>`

    ![Query for getting the service principal that you need to modify](./media/active-directory-enterprise-app-role-management/graph-explorer-new2.png)

5. <span data-ttu-id="41f28-210">Extract the **appRoles** property from the service principal object.</span><span class="sxs-lookup"><span data-stu-id="41f28-210">Extract the **appRoles** property from the service principal object.</span></span>

    ![Details of the appRoles property](./media/active-directory-enterprise-app-role-management/graph-explorer-new3.png)

6. <span data-ttu-id="41f28-212">To update the existing role, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="41f28-212">To update the existing role, use the following steps.</span></span>

    ![Request body for "PATCH," with "description" and "displayname" highlighted](./media/active-directory-enterprise-app-role-management/graph-explorer-patchupdate.png)

    <span data-ttu-id="41f28-214">a.</span><span class="sxs-lookup"><span data-stu-id="41f28-214">a.</span></span> <span data-ttu-id="41f28-215">Change the method from **GET** to **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="41f28-215">Change the method from **GET** to **PATCH**.</span></span>

    <span data-ttu-id="41f28-216">b.</span><span class="sxs-lookup"><span data-stu-id="41f28-216">b.</span></span> <span data-ttu-id="41f28-217">Copy the existing roles and paste them under **Request Body**.</span><span class="sxs-lookup"><span data-stu-id="41f28-217">Copy the existing roles and paste them under **Request Body**.</span></span>

    <span data-ttu-id="41f28-218">c.</span><span class="sxs-lookup"><span data-stu-id="41f28-218">c.</span></span> <span data-ttu-id="41f28-219">Update the value of a role by updating the role description, role value, or role display name as needed.</span><span class="sxs-lookup"><span data-stu-id="41f28-219">Update the value of a role by updating the role description, role value, or role display name as needed.</span></span>

    <span data-ttu-id="41f28-220">d.</span><span class="sxs-lookup"><span data-stu-id="41f28-220">d.</span></span> <span data-ttu-id="41f28-221">After you update all the required roles, select **Run Query**.</span><span class="sxs-lookup"><span data-stu-id="41f28-221">After you update all the required roles, select **Run Query**.</span></span>

## <a name="delete-an-existing-role"></a><span data-ttu-id="41f28-222">Delete an existing role</span><span class="sxs-lookup"><span data-stu-id="41f28-222">Delete an existing role</span></span>

<span data-ttu-id="41f28-223">To delete an  existing role, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="41f28-223">To delete an  existing role, perform the following steps:</span></span>

1. <span data-ttu-id="41f28-224">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window.</span><span class="sxs-lookup"><span data-stu-id="41f28-224">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window.</span></span>

2. <span data-ttu-id="41f28-225">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="41f28-225">Sign in to the Graph Explorer site by using the global admin or coadmin credentials for your tenant.</span></span>

3. <span data-ttu-id="41f28-226">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span><span class="sxs-lookup"><span data-stu-id="41f28-226">Change the version to **beta**, and fetch the list of service principals from your tenant by using the following query:</span></span>

    `https://graph.microsoft.com/beta/servicePrincipals`

    <span data-ttu-id="41f28-227">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span><span class="sxs-lookup"><span data-stu-id="41f28-227">If you're using multiple directories, follow this pattern: `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span></span>

    ![Graph Explorer dialog box, with the query for fetching the list of service principals](./media/active-directory-enterprise-app-role-management/graph-explorer-new1.png)

4. <span data-ttu-id="41f28-229">From the list of fetched service principals, get the one that you need to modify.</span><span class="sxs-lookup"><span data-stu-id="41f28-229">From the list of fetched service principals, get the one that you need to modify.</span></span> <span data-ttu-id="41f28-230">You can also use Ctrl+F to search the application from all the listed service principals.</span><span class="sxs-lookup"><span data-stu-id="41f28-230">You can also use Ctrl+F to search the application from all the listed service principals.</span></span> <span data-ttu-id="41f28-231">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span><span class="sxs-lookup"><span data-stu-id="41f28-231">Search for the object ID that you copied from the **Properties** page, and use the following query to get to the service principal:</span></span>

    `https://graph.microsoft.com/beta/servicePrincipals/<objectID>`

    ![Query for getting the service principal that you need to modify](./media/active-directory-enterprise-app-role-management/graph-explorer-new2.png)

5. <span data-ttu-id="41f28-233">Extract the **appRoles** property from the service principal object.</span><span class="sxs-lookup"><span data-stu-id="41f28-233">Extract the **appRoles** property from the service principal object.</span></span>

    ![Details of the appRoles property from the service principal object](./media/active-directory-enterprise-app-role-management/graph-explorer-new7.png)

6. <span data-ttu-id="41f28-235">To delete the existing role, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="41f28-235">To delete the existing role, use the following steps.</span></span>

    ![Request body for "PATCH," with IsEnabled set to false](./media/active-directory-enterprise-app-role-management/graph-explorer-new8.png)

    <span data-ttu-id="41f28-237">a.</span><span class="sxs-lookup"><span data-stu-id="41f28-237">a.</span></span> <span data-ttu-id="41f28-238">Change the method from **GET** to **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="41f28-238">Change the method from **GET** to **PATCH**.</span></span>

    <span data-ttu-id="41f28-239">b.</span><span class="sxs-lookup"><span data-stu-id="41f28-239">b.</span></span> <span data-ttu-id="41f28-240">Copy the existing roles from the application and paste them under **Request Body**.</span><span class="sxs-lookup"><span data-stu-id="41f28-240">Copy the existing roles from the application and paste them under **Request Body**.</span></span>

    <span data-ttu-id="41f28-241">c.</span><span class="sxs-lookup"><span data-stu-id="41f28-241">c.</span></span> <span data-ttu-id="41f28-242">Set the **IsEnabled** value to **false** for the role that you want to  delete.</span><span class="sxs-lookup"><span data-stu-id="41f28-242">Set the **IsEnabled** value to **false** for the role that you want to  delete.</span></span>

    <span data-ttu-id="41f28-243">d.</span><span class="sxs-lookup"><span data-stu-id="41f28-243">d.</span></span> <span data-ttu-id="41f28-244">Select **Run Query**.</span><span class="sxs-lookup"><span data-stu-id="41f28-244">Select **Run Query**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41f28-245">Make sure that you have the msiam_access role, and the ID is matching in the generated role.</span><span class="sxs-lookup"><span data-stu-id="41f28-245">Make sure that you have the msiam_access role, and the ID is matching in the generated role.</span></span>

7. <span data-ttu-id="41f28-246">After the role is disabled, delete that role block from the **appRoles** section.</span><span class="sxs-lookup"><span data-stu-id="41f28-246">After the role is disabled, delete that role block from the **appRoles** section.</span></span> <span data-ttu-id="41f28-247">Keep the method as **PATCH**, and select **Run Query**.</span><span class="sxs-lookup"><span data-stu-id="41f28-247">Keep the method as **PATCH**, and select **Run Query**.</span></span>

8. <span data-ttu-id="41f28-248">After you run the query, the role is deleted.</span><span class="sxs-lookup"><span data-stu-id="41f28-248">After you run the query, the role is deleted.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41f28-249">The role needs to be disabled before it can be removed.</span><span class="sxs-lookup"><span data-stu-id="41f28-249">The role needs to be disabled before it can be removed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41f28-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="41f28-250">Next steps</span></span>

<span data-ttu-id="41f28-251">For additional steps, see the [app documentation](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="41f28-251">For additional steps, see the [app documentation](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<!--Image references-->
<!--Image references-->

[1]: ./media/active-directory-enterprise-app-role-management/tutorial_general_01.png
[2]: ./media/active-directory-enterprise-app-role-management/tutorial_general_02.png
[3]: ./media/active-directory-enterprise-app-role-management/tutorial_general_03.png
[4]: ./media/active-directory-enterprise-app-role-management/tutorial_general_04.png