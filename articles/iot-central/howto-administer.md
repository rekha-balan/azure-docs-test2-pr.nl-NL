---
title: Administer an Azure IoT Central application | Microsoft Docs
description: As an adminstrator, how to administer your Azure IoT Central application
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: a43febf1e78f80451b6aeed19e095b2c313d3216
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868002"
---
# <a name="how-to-administer-your-application"></a><span data-ttu-id="f5bc9-103">How to administer your application</span><span class="sxs-lookup"><span data-stu-id="f5bc9-103">How to administer your application</span></span>

<span data-ttu-id="f5bc9-104">After you create a Microsoft Azure IoT Central application, you can use the **Administration** section of the Azure IoT Central user interface to administer it.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-104">After you create a Microsoft Azure IoT Central application, you can use the **Administration** section of the Azure IoT Central user interface to administer it.</span></span> <span data-ttu-id="f5bc9-105">To navigate to the **Administration** section, choose **Administration** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-105">To navigate to the **Administration** section, choose **Administration** on the left navigation menu.</span></span>

<span data-ttu-id="f5bc9-106">The **Administration** section enables you to:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-106">The **Administration** section enables you to:</span></span>

- <span data-ttu-id="f5bc9-107">Manage users</span><span class="sxs-lookup"><span data-stu-id="f5bc9-107">Manage users</span></span>

- <span data-ttu-id="f5bc9-108">Manage roles</span><span class="sxs-lookup"><span data-stu-id="f5bc9-108">Manage roles</span></span>

- <span data-ttu-id="f5bc9-109">View billing information</span><span class="sxs-lookup"><span data-stu-id="f5bc9-109">View billing information</span></span>

- <span data-ttu-id="f5bc9-110">Manage application settings</span><span class="sxs-lookup"><span data-stu-id="f5bc9-110">Manage application settings</span></span>

- <span data-ttu-id="f5bc9-111">Extend a free trial</span><span class="sxs-lookup"><span data-stu-id="f5bc9-111">Extend a free trial</span></span>

<span data-ttu-id="f5bc9-112">In the **Administration** section, there is a secondary navigation menu with links to the various administration tasks.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-112">In the **Administration** section, there is a secondary navigation menu with links to the various administration tasks.</span></span>

<span data-ttu-id="f5bc9-113">To access and use the **Administration** section, you must be in the **Administrator** role in the Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-113">To access and use the **Administration** section, you must be in the **Administrator** role in the Azure IoT Central application.</span></span> <span data-ttu-id="f5bc9-114">If you create an Azure IoT Central application, you are automatically assigned to the **Administrator** role for that application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-114">If you create an Azure IoT Central application, you are automatically assigned to the **Administrator** role for that application.</span></span> <span data-ttu-id="f5bc9-115">The *Managing Users* section in this article explains more about how to assign the **Administrator** role to other users.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-115">The *Managing Users* section in this article explains more about how to assign the **Administrator** role to other users.</span></span>

## <a name="change-application-name"></a><span data-ttu-id="f5bc9-116">Change application name</span><span class="sxs-lookup"><span data-stu-id="f5bc9-116">Change application name</span></span>

<span data-ttu-id="f5bc9-117">To change the name of your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-117">To change the name of your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span></span>

<span data-ttu-id="f5bc9-118">On the **Application Settings** page, enter a name of your choice in the **Application Name** field, and then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-118">On the **Application Settings** page, enter a name of your choice in the **Application Name** field, and then choose **Save**.</span></span>

## <a name="change-the-application-url"></a><span data-ttu-id="f5bc9-119">Change the application URL</span><span class="sxs-lookup"><span data-stu-id="f5bc9-119">Change the application URL</span></span>

<span data-ttu-id="f5bc9-120">To change the URL for your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-120">To change the URL for your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span></span>

![Application Settings Page](media\howto-administer\image0-a.png)

<span data-ttu-id="f5bc9-122">On the **Application Settings** page, enter the URL of your choice in the **URL** field, and then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-122">On the **Application Settings** page, enter the URL of your choice in the **URL** field, and then choose **Save**.</span></span> <span data-ttu-id="f5bc9-123">Your URL can be at most 200 characters in length.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-123">Your URL can be at most 200 characters in length.</span></span> <span data-ttu-id="f5bc9-124">If the URL is not available, you see a validation error</span><span class="sxs-lookup"><span data-stu-id="f5bc9-124">If the URL is not available, you see a validation error</span></span>

> [!Note]
> <span data-ttu-id="f5bc9-125">If you change your URL, your old URL can be taken by another Azure IoT Central customer.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-125">If you change your URL, your old URL can be taken by another Azure IoT Central customer.</span></span> <span data-ttu-id="f5bc9-126">In that case, it is no longer available for you to use.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-126">In that case, it is no longer available for you to use.</span></span> <span data-ttu-id="f5bc9-127">When you change your URL, the old URL no longer works and you must notify your users about the new URL to use.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-127">When you change your URL, the old URL no longer works and you must notify your users about the new URL to use.</span></span>

## <a name="change-the-application-image"></a><span data-ttu-id="f5bc9-128">Change the application image</span><span class="sxs-lookup"><span data-stu-id="f5bc9-128">Change the application image</span></span>

<span data-ttu-id="f5bc9-129">For more information about using images in an Azure IoT Central application, see [Prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span><span class="sxs-lookup"><span data-stu-id="f5bc9-129">For more information about using images in an Azure IoT Central application, see [Prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span></span>

## <a name="copy-an-application"></a><span data-ttu-id="f5bc9-130">Copy an application</span><span class="sxs-lookup"><span data-stu-id="f5bc9-130">Copy an application</span></span>

<span data-ttu-id="f5bc9-131">You can create a copy of any application, minus any device instances, device data history, and user data.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-131">You can create a copy of any application, minus any device instances, device data history, and user data.</span></span> <span data-ttu-id="f5bc9-132">The copy will be a paid application that you'll be charged for.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-132">The copy will be a paid application that you'll be charged for.</span></span> <span data-ttu-id="f5bc9-133">You cannot create a trial application by copying another application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-133">You cannot create a trial application by copying another application.</span></span>

<span data-ttu-id="f5bc9-134">To copy an application, navigate to the **Application Settings** page and click the **Copy** button.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-134">To copy an application, navigate to the **Application Settings** page and click the **Copy** button.</span></span>

![Application Settings page](media\howto-administer\appCopy1.png)

<span data-ttu-id="f5bc9-136">Clicking the **Copy** button will open a dialog in which you can select a name, URL, AAD directory, subscription and Azure region for the new application that will be created by copying your application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-136">Clicking the **Copy** button will open a dialog in which you can select a name, URL, AAD directory, subscription and Azure region for the new application that will be created by copying your application.</span></span> <span data-ttu-id="f5bc9-137">Select values for each of those fields and then click the **Copy** button to confirm that you want to proceed.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-137">Select values for each of those fields and then click the **Copy** button to confirm that you want to proceed.</span></span> <span data-ttu-id="f5bc9-138">You can learn more about what to enter for those values in the article about [how to create an application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="f5bc9-138">You can learn more about what to enter for those values in the article about [how to create an application](howto-create-application.md).</span></span>

![Application Settings page](media\howto-administer\appCopy2.png)

<span data-ttu-id="f5bc9-140">Once the app copy operation succeeds, you will be able to navigate to the new application that was created by copying your application by clicking the link that appears on the **Application Settings** page.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-140">Once the app copy operation succeeds, you will be able to navigate to the new application that was created by copying your application by clicking the link that appears on the **Application Settings** page.</span></span>

![Application Settings page](media\howto-administer\appCopy3.png)

> [!Note]
> <span data-ttu-id="f5bc9-142">Copying an application will copy the definition of rules or actions.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-142">Copying an application will copy the definition of rules or actions.</span></span> <span data-ttu-id="f5bc9-143">However, since users that have access to your original app aren't copied to the copied app, you'll have to manually add users to actions such as email for which users are a pre-requisite.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-143">However, since users that have access to your original app aren't copied to the copied app, you'll have to manually add users to actions such as email for which users are a pre-requisite.</span></span>

## <a name="delete-an-application"></a><span data-ttu-id="f5bc9-144">Delete an application</span><span class="sxs-lookup"><span data-stu-id="f5bc9-144">Delete an application</span></span>

<span data-ttu-id="f5bc9-145">To delete your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-145">To delete your application, use the secondary navigation menu to navigate to the **Application Settings** page in the **Administration** section.</span></span>

<span data-ttu-id="f5bc9-146">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-146">Choose **Delete**.</span></span>

> [!Note]
> <span data-ttu-id="f5bc9-147">Deleting an application irrecoverably deletes all data associated with the application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-147">Deleting an application irrecoverably deletes all data associated with the application.</span></span> <span data-ttu-id="f5bc9-148">To delete an application, you must also have the rights to delete resources in the Azure subscription you chose when you created the application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-148">To delete an application, you must also have the rights to delete resources in the Azure subscription you chose when you created the application.</span></span> <span data-ttu-id="f5bc9-149">To learn more, see [Use Role-Based Access Control to manage access to your Azure subscription resources](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).</span><span class="sxs-lookup"><span data-stu-id="f5bc9-149">To learn more, see [Use Role-Based Access Control to manage access to your Azure subscription resources](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).</span></span>

## <a name="roles-in-azure-iot-central"></a><span data-ttu-id="f5bc9-150">Roles in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="f5bc9-150">Roles in Azure IoT Central</span></span>

<span data-ttu-id="f5bc9-151">Roles enable you to control who, within your organization, can perform various Azure IoT Central tasks.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-151">Roles enable you to control who, within your organization, can perform various Azure IoT Central tasks.</span></span> <span data-ttu-id="f5bc9-152">Azure IoT Central has three roles you can assign to users of your application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-152">Azure IoT Central has three roles you can assign to users of your application.</span></span> <span data-ttu-id="f5bc9-153">Roles are assigned by each application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-153">Roles are assigned by each application.</span></span> <span data-ttu-id="f5bc9-154">The same user can have different roles in different applications.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-154">The same user can have different roles in different applications.</span></span> <span data-ttu-id="f5bc9-155">You can assign the same user can to multiple roles within an application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-155">You can assign the same user can to multiple roles within an application.</span></span>

### <a name="administrator"></a><span data-ttu-id="f5bc9-156">Administrator</span><span class="sxs-lookup"><span data-stu-id="f5bc9-156">Administrator</span></span>

<span data-ttu-id="f5bc9-157">Users in the **Administrator** role have access to all functionality in an Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-157">Users in the **Administrator** role have access to all functionality in an Azure IoT Central application.</span></span>

<span data-ttu-id="f5bc9-158">The user creating an application is automatically assigned to the **Administrator** role.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-158">The user creating an application is automatically assigned to the **Administrator** role.</span></span> <span data-ttu-id="f5bc9-159">There must always be at least one user in the **Administrator** role.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-159">There must always be at least one user in the **Administrator** role.</span></span>

### <a name="application-builder"></a><span data-ttu-id="f5bc9-160">Application Builder</span><span class="sxs-lookup"><span data-stu-id="f5bc9-160">Application Builder</span></span>

<span data-ttu-id="f5bc9-161">Users in the **Application Builder** role can do everything in an Azure IoT Central application except administer the application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-161">Users in the **Application Builder** role can do everything in an Azure IoT Central application except administer the application.</span></span>

### <a name="application-operator"></a><span data-ttu-id="f5bc9-162">Application Operator</span><span class="sxs-lookup"><span data-stu-id="f5bc9-162">Application Operator</span></span>

<span data-ttu-id="f5bc9-163">Users in the **Application Operator** role don't have access to the **Application Builder** page.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-163">Users in the **Application Operator** role don't have access to the **Application Builder** page.</span></span> <span data-ttu-id="f5bc9-164">They can't administer the application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-164">They can't administer the application.</span></span>

## <a name="manage-users"></a><span data-ttu-id="f5bc9-165">Manage users</span><span class="sxs-lookup"><span data-stu-id="f5bc9-165">Manage users</span></span>

<span data-ttu-id="f5bc9-166">Application administrators can assign users to the roles in the application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-166">Application administrators can assign users to the roles in the application.</span></span>

### <a name="add-users"></a><span data-ttu-id="f5bc9-167">Add users</span><span class="sxs-lookup"><span data-stu-id="f5bc9-167">Add users</span></span>

<span data-ttu-id="f5bc9-168">Every user must have a user account before they can sign in and access an Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-168">Every user must have a user account before they can sign in and access an Azure IoT Central application.</span></span> <span data-ttu-id="f5bc9-169">Microsoft Accounts (MSAs) and Azure Active Directory (AAD) accounts are supported in Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-169">Microsoft Accounts (MSAs) and Azure Active Directory (AAD) accounts are supported in Azure IoT Central.</span></span> <span data-ttu-id="f5bc9-170">Azure Active Directory groups are not currently supported in Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-170">Azure Active Directory groups are not currently supported in Azure IoT Central.</span></span>

<span data-ttu-id="f5bc9-171">To learn more, see [Microsoft account help](https://support.microsoft.com/products/microsoft-account?category=manage-account) and  [Quickstart: Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory).</span><span class="sxs-lookup"><span data-stu-id="f5bc9-171">To learn more, see [Microsoft account help](https://support.microsoft.com/products/microsoft-account?category=manage-account) and  [Quickstart: Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory).</span></span>

1. <span data-ttu-id="f5bc9-172">To add a user account to an Azure IoT Central application, use the secondary navigation menu to navigate to the **Users** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-172">To add a user account to an Azure IoT Central application, use the secondary navigation menu to navigate to the **Users** page in the **Administration** section.</span></span>

    ![List of Users](media\howto-administer\image1.png)

1. <span data-ttu-id="f5bc9-174">On the **Users** page, choose **+ Add user** to add a user.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-174">On the **Users** page, choose **+ Add user** to add a user.</span></span>

    ![Add User](media\howto-administer\image2.png)

1. <span data-ttu-id="f5bc9-176">When you add a user to your Azure IoT Central application, choose a role for the user from the **Role** drop-down.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-176">When you add a user to your Azure IoT Central application, choose a role for the user from the **Role** drop-down.</span></span> <span data-ttu-id="f5bc9-177">Learn more about roles in the *Roles in Azure IoT Central* section of this article.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-177">Learn more about roles in the *Roles in Azure IoT Central* section of this article.</span></span>

    ![Role Selection](media\howto-administer\image3.png)

    > [!NOTE]
    >  <span data-ttu-id="f5bc9-179">To add users in bulk, enter the User IDs of all the users you'd like to add separated by semi-colons.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-179">To add users in bulk, enter the User IDs of all the users you'd like to add separated by semi-colons.</span></span> <span data-ttu-id="f5bc9-180">Choose a role from the **Role** drop-down and choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-180">Choose a role from the **Role** drop-down and choose **Save**.</span></span>

1. <span data-ttu-id="f5bc9-181">After you add a user, an entry appears for that user on the **Users** page.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-181">After you add a user, an entry appears for that user on the **Users** page.</span></span>

    ![User List](media\howto-administer\image4.png)

### <a name="edit-the-roles-assigned-to-users"></a><span data-ttu-id="f5bc9-183">Edit the roles assigned to users</span><span class="sxs-lookup"><span data-stu-id="f5bc9-183">Edit the roles assigned to users</span></span>

<span data-ttu-id="f5bc9-184">Roles cannot be changed once assinged.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-184">Roles cannot be changed once assinged.</span></span> <span data-ttu-id="f5bc9-185">To change the role assigned to a user, delete the user and add the user again with a different role.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-185">To change the role assigned to a user, delete the user and add the user again with a different role.</span></span>

### <a name="delete-users"></a><span data-ttu-id="f5bc9-186">Delete users</span><span class="sxs-lookup"><span data-stu-id="f5bc9-186">Delete users</span></span>

<span data-ttu-id="f5bc9-187">To delete users, check one or more checkboxes on the **Users** page and then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-187">To delete users, check one or more checkboxes on the **Users** page and then choose **Delete**.</span></span>

## <a name="view-your-bill"></a><span data-ttu-id="f5bc9-188">View your bill</span><span class="sxs-lookup"><span data-stu-id="f5bc9-188">View your bill</span></span>

<span data-ttu-id="f5bc9-189">To view your bill, navigate to the **Billing** page in the **Administration** section and choose **Billing**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-189">To view your bill, navigate to the **Billing** page in the **Administration** section and choose **Billing**.</span></span> <span data-ttu-id="f5bc9-190">The Azure billing page opens in a new tab and you can see the bill for each of your Azure IoT Central applications.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-190">The Azure billing page opens in a new tab and you can see the bill for each of your Azure IoT Central applications.</span></span>

## <a name="convert-your-trial-to-a-paid-application"></a><span data-ttu-id="f5bc9-191">Convert your trial to a paid application</span><span class="sxs-lookup"><span data-stu-id="f5bc9-191">Convert your trial to a paid application</span></span>

<span data-ttu-id="f5bc9-192">Once you've evaluated IoT Central, you can convert your trial to a paid application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-192">Once you've evaluated IoT Central, you can convert your trial to a paid application.</span></span> <span data-ttu-id="f5bc9-193">To complete this self-service process, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-193">To complete this self-service process, follow these steps:</span></span>

1. <span data-ttu-id="f5bc9-194">Use the secondary navigation menu to navigate to the **Billing** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-194">Use the secondary navigation menu to navigate to the **Billing** page in the **Administration** section.</span></span> <span data-ttu-id="f5bc9-195">If you haven't extended your trial, the page looks like the following:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-195">If you haven't extended your trial, the page looks like the following:</span></span>

    ![Free trial state](media/howto-administer/freetrial.png)

2. <span data-ttu-id="f5bc9-197">Click **Convert to Paid**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-197">Click **Convert to Paid**.</span></span> <span data-ttu-id="f5bc9-198">If you haven't extended your trial, the pop-up looks like the following:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-198">If you haven't extended your trial, the pop-up looks like the following:</span></span>

    <span data-ttu-id="f5bc9-199">In the pop-up select the appropriate Azure Active Directory tenant and then the Azure Subscription that you want to use for your IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-199">In the pop-up select the appropriate Azure Active Directory tenant and then the Azure Subscription that you want to use for your IoT Central application.</span></span>

    ![Extend free trial](media/howto-administer/extend.png)

3. <span data-ttu-id="f5bc9-201">After you click **Convert**, your trial is converted to a paid application and you start getting billed.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-201">After you click **Convert**, your trial is converted to a paid application and you start getting billed.</span></span>

## <a name="extend-your-free-trial"></a><span data-ttu-id="f5bc9-202">Extend your free trial</span><span class="sxs-lookup"><span data-stu-id="f5bc9-202">Extend your free trial</span></span>

<span data-ttu-id="f5bc9-203">By default, all free trials are available for 7 days.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-203">By default, all free trials are available for 7 days.</span></span> <span data-ttu-id="f5bc9-204">If you'd like to increase your trial to 30 days, you follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-204">If you'd like to increase your trial to 30 days, you follow these steps:</span></span>

1. <span data-ttu-id="f5bc9-205">Use the secondary navigation menu to navigate to the **Billing** page in the **Administration** section:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-205">Use the secondary navigation menu to navigate to the **Billing** page in the **Administration** section:</span></span>

1. <span data-ttu-id="f5bc9-206">Click **Extend Trial**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-206">Click **Extend Trial**.</span></span> <span data-ttu-id="f5bc9-207">In the pop-up select the appropriate Azure Active Directory tenant and then the Azure Subscription to use for your IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-207">In the pop-up select the appropriate Azure Active Directory tenant and then the Azure Subscription to use for your IoT Central application:</span></span>

1. <span data-ttu-id="f5bc9-208">Then click **Extend**.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-208">Then click **Extend**.</span></span> <span data-ttu-id="f5bc9-209">Your trial is now valid for 30 days.</span><span class="sxs-lookup"><span data-stu-id="f5bc9-209">Your trial is now valid for 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5bc9-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5bc9-210">Next steps</span></span>

<span data-ttu-id="f5bc9-211">Now that you have learned how to administer your Azure IoT Central application, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="f5bc9-211">Now that you have learned how to administer your Azure IoT Central application, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5bc9-212">Set up the device template</span><span class="sxs-lookup"><span data-stu-id="f5bc9-212">Set up the device template</span></span>](howto-set-up-template.md)