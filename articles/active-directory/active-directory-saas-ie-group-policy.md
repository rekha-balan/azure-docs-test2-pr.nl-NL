---
title: Deploy Azure Access Panel Extension for IE using a GPO | Microsoft Docs
description: How to use group policy to deploy the Internet Explorer add-on for the My Apps portal.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 81150281acef7d79dee578f31f4e5b8838f5726b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552616"
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="bc236-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span><span class="sxs-lookup"><span data-stu-id="bc236-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="bc236-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span><span class="sxs-lookup"><span data-stu-id="bc236-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="bc236-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bc236-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="bc236-106">It is recommended that admins automate the deployment of this extension.</span><span class="sxs-lookup"><span data-stu-id="bc236-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="bc236-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="bc236-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="bc236-108">This tutorial covers one method of automating software deployments by using group policy.</span><span class="sxs-lookup"><span data-stu-id="bc236-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="bc236-109">Learn more about group policy.</span><span class="sxs-lookup"><span data-stu-id="bc236-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="bc236-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span><span class="sxs-lookup"><span data-stu-id="bc236-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc236-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc236-111">Prerequisites</span></span>
* <span data-ttu-id="bc236-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span><span class="sxs-lookup"><span data-stu-id="bc236-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="bc236-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span><span class="sxs-lookup"><span data-stu-id="bc236-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="bc236-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="bc236-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="bc236-115">Learn more.</span><span class="sxs-lookup"><span data-stu-id="bc236-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="bc236-116">Step 1: Create the Distribution Point</span><span class="sxs-lookup"><span data-stu-id="bc236-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="bc236-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span><span class="sxs-lookup"><span data-stu-id="bc236-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="bc236-118">To do this, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bc236-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="bc236-119">Log on to the server as an administrator</span><span class="sxs-lookup"><span data-stu-id="bc236-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="bc236-120">In the **Server Manager** window, go to **Files and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="bc236-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Open Files and Storage Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="bc236-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span><span class="sxs-lookup"><span data-stu-id="bc236-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Open Files and Storage Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="bc236-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span><span class="sxs-lookup"><span data-stu-id="bc236-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="bc236-125">Learn more about shares.</span><span class="sxs-lookup"><span data-stu-id="bc236-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="bc236-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="bc236-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="bc236-127">Copy the installer package to a desired location on the share.</span><span class="sxs-lookup"><span data-stu-id="bc236-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Copy the .msi file to the share.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="bc236-129">Verify that your client machines are able to access the installer package from the share.</span><span class="sxs-lookup"><span data-stu-id="bc236-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="bc236-130">Step 2: Create the Group Policy Object</span><span class="sxs-lookup"><span data-stu-id="bc236-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="bc236-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span><span class="sxs-lookup"><span data-stu-id="bc236-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="bc236-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="bc236-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Go to Tools > Group Policy Managment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="bc236-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span><span class="sxs-lookup"><span data-stu-id="bc236-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="bc236-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span><span class="sxs-lookup"><span data-stu-id="bc236-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bc236-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="bc236-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="bc236-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span><span class="sxs-lookup"><span data-stu-id="bc236-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Create a new GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="bc236-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span><span class="sxs-lookup"><span data-stu-id="bc236-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Name the new GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="bc236-141">Right-click the Group Policy Object that you created, and select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="bc236-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Edit the new GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="bc236-143">Step 3: Assign the Installation Package</span><span class="sxs-lookup"><span data-stu-id="bc236-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="bc236-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span><span class="sxs-lookup"><span data-stu-id="bc236-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="bc236-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span><span class="sxs-lookup"><span data-stu-id="bc236-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="bc236-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span><span class="sxs-lookup"><span data-stu-id="bc236-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="bc236-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span><span class="sxs-lookup"><span data-stu-id="bc236-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="bc236-148">Right-click **Software installation**, then select **New** > **Package...**</span><span class="sxs-lookup"><span data-stu-id="bc236-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Create a new software installation package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="bc236-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span><span class="sxs-lookup"><span data-stu-id="bc236-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bc236-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span><span class="sxs-lookup"><span data-stu-id="bc236-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Select the installation package from the shared folder.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="bc236-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span><span class="sxs-lookup"><span data-stu-id="bc236-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="bc236-154">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc236-154">Then click **OK**.</span></span>
   
    ![Select Assigned, then click OK.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="bc236-156">The extension is now deployed to the OU that you selected.</span><span class="sxs-lookup"><span data-stu-id="bc236-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="bc236-157">Learn more about Group Policy Software Installation.</span><span class="sxs-lookup"><span data-stu-id="bc236-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="bc236-158">Step 4: Auto-Enable the Extension for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="bc236-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="bc236-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span><span class="sxs-lookup"><span data-stu-id="bc236-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="bc236-160">Follow the steps below to enable the Access Panel Extension using group policy:</span><span class="sxs-lookup"><span data-stu-id="bc236-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="bc236-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="bc236-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="bc236-162">Right-click **Add-on List**, and select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="bc236-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="bc236-163">![Edit Add-on List.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="bc236-163">![Edit Add-on List.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="bc236-164">In the **Add-on List** window, select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="bc236-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="bc236-165">Then, under the **Options** section, click **Show...**.</span><span class="sxs-lookup"><span data-stu-id="bc236-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Click Enable, then click Show...](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="bc236-167">In the **Show Contents** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc236-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="bc236-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="bc236-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="bc236-169">For the second column (the **Value** field), type in the following value: `1`</span><span class="sxs-lookup"><span data-stu-id="bc236-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="bc236-170">Click **OK** to close the **Show Contents** window.</span><span class="sxs-lookup"><span data-stu-id="bc236-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Fill out the values as specified above.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="bc236-172">Click **OK** to apply your changes and close the **Add-on List** window.</span><span class="sxs-lookup"><span data-stu-id="bc236-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="bc236-173">The extension should now be enabled for the machines in the selected OU.</span><span class="sxs-lookup"><span data-stu-id="bc236-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="bc236-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span><span class="sxs-lookup"><span data-stu-id="bc236-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="bc236-175">Step 5 (Optional): Disable "Remember Password" Prompt</span><span class="sxs-lookup"><span data-stu-id="bc236-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="bc236-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span><span class="sxs-lookup"><span data-stu-id="bc236-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="bc236-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span><span class="sxs-lookup"><span data-stu-id="bc236-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="bc236-178">In the **Group Policy Management Editor** window, go to the path listed below.</span><span class="sxs-lookup"><span data-stu-id="bc236-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="bc236-179">This configuration setting is only available under **User Configuration**.</span><span class="sxs-lookup"><span data-stu-id="bc236-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="bc236-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span><span class="sxs-lookup"><span data-stu-id="bc236-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bc236-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span><span class="sxs-lookup"><span data-stu-id="bc236-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="bc236-182">The configuration for that setting differs from the setting described in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bc236-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Remember to look for this under User Settings.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="bc236-184">Right click the above setting, and select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="bc236-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="bc236-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="bc236-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Select Disable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="bc236-187">Click **OK** to apply these changes and close the window.</span><span class="sxs-lookup"><span data-stu-id="bc236-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="bc236-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span><span class="sxs-lookup"><span data-stu-id="bc236-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="bc236-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span><span class="sxs-lookup"><span data-stu-id="bc236-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="bc236-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span><span class="sxs-lookup"><span data-stu-id="bc236-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="bc236-191">Step 6: Testing the Deployment</span><span class="sxs-lookup"><span data-stu-id="bc236-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="bc236-192">Follow the steps below to verify if the extension deployment was successful:</span><span class="sxs-lookup"><span data-stu-id="bc236-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="bc236-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="bc236-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="bc236-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span><span class="sxs-lookup"><span data-stu-id="bc236-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="bc236-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span><span class="sxs-lookup"><span data-stu-id="bc236-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="bc236-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="bc236-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="bc236-197">You must restart the machine for the installation to take place.</span><span class="sxs-lookup"><span data-stu-id="bc236-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="bc236-198">Bootup may take significantly more time than usual while the extension installs.</span><span class="sxs-lookup"><span data-stu-id="bc236-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="bc236-199">After restarting, open **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bc236-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="bc236-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span><span class="sxs-lookup"><span data-stu-id="bc236-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Go to Tools > Manage Add-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="bc236-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="bc236-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Verify that the Access Panel Extension is installed and enabled.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="bc236-204">Related Articles</span><span class="sxs-lookup"><span data-stu-id="bc236-204">Related Articles</span></span>
* [<span data-ttu-id="bc236-205">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc236-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="bc236-206">Application access and single sign-on with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc236-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bc236-207">Troubleshooting the Access Panel Extension for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="bc236-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)


















