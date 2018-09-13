---
title: Configure your API Management service using Git - Azure | Microsoft Docs
description: Learn how to save and configure your API Management service configuration using Git.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 3b0824fe628dc88f5bce4eb5e69bcc0a01efcb66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552570"
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="e6976-103">How to save and configure your API Management service configuration using Git</span><span class="sxs-lookup"><span data-stu-id="e6976-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="e6976-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="e6976-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span><span class="sxs-lookup"><span data-stu-id="e6976-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="e6976-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="e6976-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="e6976-107">Configuration versioning - download and store different versions of your service configuration</span><span class="sxs-lookup"><span data-stu-id="e6976-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="e6976-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span><span class="sxs-lookup"><span data-stu-id="e6976-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="e6976-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span><span class="sxs-lookup"><span data-stu-id="e6976-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="e6976-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Git configure][api-management-git-configure]

<span data-ttu-id="e6976-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span><span class="sxs-lookup"><span data-stu-id="e6976-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="e6976-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="e6976-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="e6976-114">The following steps provide an overview of managing your API Management service instance using Git.</span><span class="sxs-lookup"><span data-stu-id="e6976-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="e6976-115">Access Git configuration in your service</span><span class="sxs-lookup"><span data-stu-id="e6976-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="e6976-116">Save your service configuration database to your Git repository</span><span class="sxs-lookup"><span data-stu-id="e6976-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="e6976-117">Clone the Git repo to your local machine</span><span class="sxs-lookup"><span data-stu-id="e6976-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="e6976-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span><span class="sxs-lookup"><span data-stu-id="e6976-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="e6976-119">Deploy the changes from your repo into your service configuration database</span><span class="sxs-lookup"><span data-stu-id="e6976-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="e6976-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="e6976-121">Access Git configuration in your service</span><span class="sxs-lookup"><span data-stu-id="e6976-121">Access Git configuration in your service</span></span>
<span data-ttu-id="e6976-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e6976-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="e6976-123">In this example, the status message indicates that there are unsaved changes to the repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="e6976-124">This is because the API Management service configuration database has not yet been saved to the repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Git status][api-management-git-icon-enable]

<span data-ttu-id="e6976-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span><span class="sxs-lookup"><span data-stu-id="e6976-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Enable GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="e6976-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span><span class="sxs-lookup"><span data-stu-id="e6976-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="e6976-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span><span class="sxs-lookup"><span data-stu-id="e6976-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="e6976-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="e6976-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="e6976-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="e6976-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="e6976-132">To save the service configuration to the Git repository</span><span class="sxs-lookup"><span data-stu-id="e6976-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="e6976-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="e6976-134">Click **Save configuration to repository**.</span><span class="sxs-lookup"><span data-stu-id="e6976-134">Click **Save configuration to repository**.</span></span>

![Save configuration][api-management-save-configuration]

<span data-ttu-id="e6976-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span><span class="sxs-lookup"><span data-stu-id="e6976-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Save configuration][api-management-save-configuration-confirm]

<span data-ttu-id="e6976-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Configuration status][api-management-configuration-status]

<span data-ttu-id="e6976-140">Once the configuration is saved to the repository, it can be cloned.</span><span class="sxs-lookup"><span data-stu-id="e6976-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="e6976-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="e6976-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="e6976-142">To clone the repository to your local machine</span><span class="sxs-lookup"><span data-stu-id="e6976-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="e6976-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span><span class="sxs-lookup"><span data-stu-id="e6976-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="e6976-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span><span class="sxs-lookup"><span data-stu-id="e6976-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Git clone][api-management-configuration-git-clone]

<span data-ttu-id="e6976-146">The password is generated at the bottom of the **Configuration repository** tab.</span><span class="sxs-lookup"><span data-stu-id="e6976-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Generate password][api-management-generate-password]

<span data-ttu-id="e6976-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span><span class="sxs-lookup"><span data-stu-id="e6976-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Password][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="e6976-150">Make a note of this password.</span><span class="sxs-lookup"><span data-stu-id="e6976-150">Make a note of this password.</span></span> <span data-ttu-id="e6976-151">Once you leave this page the password will not be displayed again.</span><span class="sxs-lookup"><span data-stu-id="e6976-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="e6976-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span><span class="sxs-lookup"><span data-stu-id="e6976-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="e6976-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e6976-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="e6976-154">Provide the user name and password when prompted.</span><span class="sxs-lookup"><span data-stu-id="e6976-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="e6976-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="e6976-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="e6976-156">If this provides an error, try URL encoding the password portion of the command.</span><span class="sxs-lookup"><span data-stu-id="e6976-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="e6976-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span><span class="sxs-lookup"><span data-stu-id="e6976-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="e6976-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="e6976-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="e6976-159">Use the encoded password along with your user name and repository location to construct the git command.</span><span class="sxs-lookup"><span data-stu-id="e6976-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="e6976-160">Once the repository is cloned you can view and work with it in your local file system.</span><span class="sxs-lookup"><span data-stu-id="e6976-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="e6976-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="e6976-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="e6976-162">To update your local repository with the most current service instance configuration</span><span class="sxs-lookup"><span data-stu-id="e6976-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="e6976-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span><span class="sxs-lookup"><span data-stu-id="e6976-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="e6976-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="e6976-165">Before running `git pull` ensure that you are in the folder for your local repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="e6976-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span><span class="sxs-lookup"><span data-stu-id="e6976-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="e6976-167">To push changes from your local repo to the server repo</span><span class="sxs-lookup"><span data-stu-id="e6976-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="e6976-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span><span class="sxs-lookup"><span data-stu-id="e6976-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="e6976-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span><span class="sxs-lookup"><span data-stu-id="e6976-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="e6976-170">To push all of the commits to the server, run the following command.</span><span class="sxs-lookup"><span data-stu-id="e6976-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="e6976-171">To deploy any service configuration changes to the API Management service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="e6976-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Deploy][api-management-configuration-deploy]

<span data-ttu-id="e6976-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="e6976-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="e6976-175">File and folder structure reference of local Git repository</span><span class="sxs-lookup"><span data-stu-id="e6976-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="e6976-176">The files and folders in the local git repository contain the configuration information about the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="e6976-177">Item</span><span class="sxs-lookup"><span data-stu-id="e6976-177">Item</span></span> | <span data-ttu-id="e6976-178">Description</span><span class="sxs-lookup"><span data-stu-id="e6976-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6976-179">root api-management folder</span><span class="sxs-lookup"><span data-stu-id="e6976-179">root api-management folder</span></span> |<span data-ttu-id="e6976-180">Contains top-level configuration for the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="e6976-181">apis folder</span><span class="sxs-lookup"><span data-stu-id="e6976-181">apis folder</span></span> |<span data-ttu-id="e6976-182">Contains the configuration for the apis in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="e6976-183">groups folder</span><span class="sxs-lookup"><span data-stu-id="e6976-183">groups folder</span></span> |<span data-ttu-id="e6976-184">Contains the configuration for the groups in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="e6976-185">policies folder</span><span class="sxs-lookup"><span data-stu-id="e6976-185">policies folder</span></span> |<span data-ttu-id="e6976-186">Contains the policies in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="e6976-187">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="e6976-187">portalStyles folder</span></span> |<span data-ttu-id="e6976-188">Contains the configuration for the developer portal customizations in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="e6976-189">products folder</span><span class="sxs-lookup"><span data-stu-id="e6976-189">products folder</span></span> |<span data-ttu-id="e6976-190">Contains the configuration for the products in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="e6976-191">templates folder</span><span class="sxs-lookup"><span data-stu-id="e6976-191">templates folder</span></span> |<span data-ttu-id="e6976-192">Contains the configuration for the email templates in the service instance</span><span class="sxs-lookup"><span data-stu-id="e6976-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="e6976-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span><span class="sxs-lookup"><span data-stu-id="e6976-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="e6976-194">The files within each folder are specific for the entity type described by the folder name.</span><span class="sxs-lookup"><span data-stu-id="e6976-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="e6976-195">File type</span><span class="sxs-lookup"><span data-stu-id="e6976-195">File type</span></span> | <span data-ttu-id="e6976-196">Purpose</span><span class="sxs-lookup"><span data-stu-id="e6976-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="e6976-197">json</span><span class="sxs-lookup"><span data-stu-id="e6976-197">json</span></span> |<span data-ttu-id="e6976-198">Configuration information about the respective entity</span><span class="sxs-lookup"><span data-stu-id="e6976-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="e6976-199">html</span><span class="sxs-lookup"><span data-stu-id="e6976-199">html</span></span> |<span data-ttu-id="e6976-200">Descriptions about the entity, often displayed in the developer portal</span><span class="sxs-lookup"><span data-stu-id="e6976-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="e6976-201">xml</span><span class="sxs-lookup"><span data-stu-id="e6976-201">xml</span></span> |<span data-ttu-id="e6976-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="e6976-202">Policy statements</span></span> |
| <span data-ttu-id="e6976-203">css</span><span class="sxs-lookup"><span data-stu-id="e6976-203">css</span></span> |<span data-ttu-id="e6976-204">Style sheets for developer portal customization</span><span class="sxs-lookup"><span data-stu-id="e6976-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="e6976-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="e6976-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span><span class="sxs-lookup"><span data-stu-id="e6976-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="e6976-207">Users</span><span class="sxs-lookup"><span data-stu-id="e6976-207">Users</span></span>
> * <span data-ttu-id="e6976-208">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="e6976-208">Subscriptions</span></span>
> * <span data-ttu-id="e6976-209">Properties</span><span class="sxs-lookup"><span data-stu-id="e6976-209">Properties</span></span>
> * <span data-ttu-id="e6976-210">Developer portal entities other than styles</span><span class="sxs-lookup"><span data-stu-id="e6976-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="e6976-211">Root api-management folder</span><span class="sxs-lookup"><span data-stu-id="e6976-211">Root api-management folder</span></span>
<span data-ttu-id="e6976-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span><span class="sxs-lookup"><span data-stu-id="e6976-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="e6976-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="e6976-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="e6976-214">Identity setting</span><span class="sxs-lookup"><span data-stu-id="e6976-214">Identity setting</span></span> | <span data-ttu-id="e6976-215">Maps to</span><span class="sxs-lookup"><span data-stu-id="e6976-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="e6976-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="e6976-216">RegistrationEnabled</span></span> |<span data-ttu-id="e6976-217">**Redirect anonymous users to sign-in page** checkbox</span><span class="sxs-lookup"><span data-stu-id="e6976-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="e6976-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="e6976-218">UserRegistrationTerms</span></span> |<span data-ttu-id="e6976-219">**Terms of use on user signup** textbox</span><span class="sxs-lookup"><span data-stu-id="e6976-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="e6976-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="e6976-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="e6976-221">**Show terms of use on signup page** checkbox</span><span class="sxs-lookup"><span data-stu-id="e6976-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="e6976-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="e6976-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="e6976-223">**Require consent** checkbox</span><span class="sxs-lookup"><span data-stu-id="e6976-223">**Require consent** checkbox</span></span> |

![Identity settings][api-management-identity-settings]

<span data-ttu-id="e6976-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="e6976-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="e6976-226">Delegation setting</span><span class="sxs-lookup"><span data-stu-id="e6976-226">Delegation setting</span></span> | <span data-ttu-id="e6976-227">Maps to</span><span class="sxs-lookup"><span data-stu-id="e6976-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="e6976-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="e6976-228">DelegationEnabled</span></span> |<span data-ttu-id="e6976-229">**Delegate sign-in & sign-up** checkbox</span><span class="sxs-lookup"><span data-stu-id="e6976-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="e6976-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="e6976-230">DelegationUrl</span></span> |<span data-ttu-id="e6976-231">**Delegation endpoint URL** textbox</span><span class="sxs-lookup"><span data-stu-id="e6976-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="e6976-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="e6976-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="e6976-233">**Delegate product subscription** checkbox</span><span class="sxs-lookup"><span data-stu-id="e6976-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="e6976-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="e6976-234">DelegationValidationKey</span></span> |<span data-ttu-id="e6976-235">**Delegate Validation Key** textbox</span><span class="sxs-lookup"><span data-stu-id="e6976-235">**Delegate Validation Key** textbox</span></span> |

![Delegation settings][api-management-delegation-settings]

<span data-ttu-id="e6976-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="e6976-238">apis folder</span><span class="sxs-lookup"><span data-stu-id="e6976-238">apis folder</span></span>
<span data-ttu-id="e6976-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span><span class="sxs-lookup"><span data-stu-id="e6976-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="e6976-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span><span class="sxs-lookup"><span data-stu-id="e6976-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="e6976-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span><span class="sxs-lookup"><span data-stu-id="e6976-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="e6976-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="e6976-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="e6976-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span><span class="sxs-lookup"><span data-stu-id="e6976-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="e6976-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span><span class="sxs-lookup"><span data-stu-id="e6976-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="e6976-245">groups folder</span><span class="sxs-lookup"><span data-stu-id="e6976-245">groups folder</span></span>
<span data-ttu-id="e6976-246">The `groups` folder contains a folder for each group defined in the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="e6976-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span><span class="sxs-lookup"><span data-stu-id="e6976-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="e6976-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span><span class="sxs-lookup"><span data-stu-id="e6976-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="e6976-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="e6976-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="e6976-250">policies folder</span><span class="sxs-lookup"><span data-stu-id="e6976-250">policies folder</span></span>
<span data-ttu-id="e6976-251">The `policies` folder contains the policy statements for your service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="e6976-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="e6976-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span><span class="sxs-lookup"><span data-stu-id="e6976-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="e6976-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span><span class="sxs-lookup"><span data-stu-id="e6976-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="e6976-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span><span class="sxs-lookup"><span data-stu-id="e6976-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="e6976-256">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="e6976-256">portalStyles folder</span></span>
<span data-ttu-id="e6976-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="e6976-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span><span class="sxs-lookup"><span data-stu-id="e6976-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="e6976-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span><span class="sxs-lookup"><span data-stu-id="e6976-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="e6976-260">products folder</span><span class="sxs-lookup"><span data-stu-id="e6976-260">products folder</span></span>
<span data-ttu-id="e6976-261">The `products` folder contains a folder for each product defined in the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="e6976-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span><span class="sxs-lookup"><span data-stu-id="e6976-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="e6976-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span><span class="sxs-lookup"><span data-stu-id="e6976-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="e6976-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span><span class="sxs-lookup"><span data-stu-id="e6976-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="e6976-265">templates</span><span class="sxs-lookup"><span data-stu-id="e6976-265">templates</span></span>
<span data-ttu-id="e6976-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span><span class="sxs-lookup"><span data-stu-id="e6976-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="e6976-267">`<template name>\configuration.json` - this is the configuration for the email template.</span><span class="sxs-lookup"><span data-stu-id="e6976-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="e6976-268">`<template name>\body.html` - this is the body of the email template.</span><span class="sxs-lookup"><span data-stu-id="e6976-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6976-269">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6976-269">Next steps</span></span>
<span data-ttu-id="e6976-270">For information on other ways to manage your service instance, see:</span><span class="sxs-lookup"><span data-stu-id="e6976-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="e6976-271">Manage your service instance using the following PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="e6976-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="e6976-272">Service deployment PowerShell cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="e6976-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="e6976-273">Service management PowerShell cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="e6976-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="e6976-274">Manage your service instance in the publisher portal</span><span class="sxs-lookup"><span data-stu-id="e6976-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="e6976-275">Manage your first API</span><span class="sxs-lookup"><span data-stu-id="e6976-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="e6976-276">Manage your service instance using the REST API</span><span class="sxs-lookup"><span data-stu-id="e6976-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="e6976-277">API Management REST API reference</span><span class="sxs-lookup"><span data-stu-id="e6976-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="e6976-278">Watch a video overview</span><span class="sxs-lookup"><span data-stu-id="e6976-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-configuration-repository-git/api-management-git-icon-enable.png

















