---
title: Configure your API Management service using Git - Azure | Microsoft Docs
description: Learn how to save and configure your API Management service configuration using Git.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: mattfarm
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2018
ms.author: apimpm
ms.openlocfilehash: 8c4ae9c7b8be8cf390ad4ad6d99cd1ec41cd3d08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809652"
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="3708f-103">How to save and configure your API Management service configuration using Git</span><span class="sxs-lookup"><span data-stu-id="3708f-103">How to save and configure your API Management service configuration using Git</span></span>

<span data-ttu-id="3708f-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="3708f-105">Changes can be made to the service instance by changing a setting in the Azure portal, using a PowerShell cmdlet, or making a REST API call.</span><span class="sxs-lookup"><span data-stu-id="3708f-105">Changes can be made to the service instance by changing a setting in the Azure portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="3708f-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="3708f-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="3708f-107">Configuration versioning - download and store different versions of your service configuration</span><span class="sxs-lookup"><span data-stu-id="3708f-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="3708f-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span><span class="sxs-lookup"><span data-stu-id="3708f-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="3708f-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span><span class="sxs-lookup"><span data-stu-id="3708f-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="3708f-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Git configure][api-management-git-configure]

<span data-ttu-id="3708f-112">When you make changes to your service using the Azure portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span><span class="sxs-lookup"><span data-stu-id="3708f-112">When you make changes to your service using the Azure portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="3708f-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="3708f-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="3708f-114">The following steps provide an overview of managing your API Management service instance using Git.</span><span class="sxs-lookup"><span data-stu-id="3708f-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="3708f-115">Access Git configuration in your service</span><span class="sxs-lookup"><span data-stu-id="3708f-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="3708f-116">Save your service configuration database to your Git repository</span><span class="sxs-lookup"><span data-stu-id="3708f-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="3708f-117">Clone the Git repo to your local machine</span><span class="sxs-lookup"><span data-stu-id="3708f-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="3708f-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span><span class="sxs-lookup"><span data-stu-id="3708f-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="3708f-119">Deploy the changes from your repo into your service configuration database</span><span class="sxs-lookup"><span data-stu-id="3708f-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="3708f-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="3708f-121">Access Git configuration in your service</span><span class="sxs-lookup"><span data-stu-id="3708f-121">Access Git configuration in your service</span></span>

<span data-ttu-id="3708f-122">To view and configure your Git configuration settings, you can click the **Security** menu and navigate to the **Configuration repository** tab.</span><span class="sxs-lookup"><span data-stu-id="3708f-122">To view and configure your Git configuration settings, you can click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Enable GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="3708f-124">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span><span class="sxs-lookup"><span data-stu-id="3708f-124">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="3708f-125">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span><span class="sxs-lookup"><span data-stu-id="3708f-125">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="3708f-126">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="3708f-126">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="3708f-127">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="3708f-127">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="3708f-128">To save the service configuration to the Git repository</span><span class="sxs-lookup"><span data-stu-id="3708f-128">To save the service configuration to the Git repository</span></span>

<span data-ttu-id="3708f-129">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-129">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="3708f-130">Click **Save to repository**.</span><span class="sxs-lookup"><span data-stu-id="3708f-130">Click **Save to repository**.</span></span>

<span data-ttu-id="3708f-131">Make any desired changes on the confirmation screen and click **Ok** to save.</span><span class="sxs-lookup"><span data-stu-id="3708f-131">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

<span data-ttu-id="3708f-132">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-132">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

<span data-ttu-id="3708f-133">Once the configuration is saved to the repository, it can be cloned.</span><span class="sxs-lookup"><span data-stu-id="3708f-133">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="3708f-134">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="3708f-134">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="3708f-135">To clone the repository to your local machine</span><span class="sxs-lookup"><span data-stu-id="3708f-135">To clone the repository to your local machine</span></span>

<span data-ttu-id="3708f-136">To clone a repository, you need the URL to your repository, a user name, and a password.</span><span class="sxs-lookup"><span data-stu-id="3708f-136">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="3708f-137">To get user name and other credentials, click on **Access credentials** near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="3708f-137">To get user name and other credentials, click on **Access credentials** near the top of the page.</span></span>  
 
<span data-ttu-id="3708f-138">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate**.</span><span class="sxs-lookup"><span data-stu-id="3708f-138">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3708f-139">Make a note of this password.</span><span class="sxs-lookup"><span data-stu-id="3708f-139">Make a note of this password.</span></span> <span data-ttu-id="3708f-140">Once you leave this page the password will not be displayed again.</span><span class="sxs-lookup"><span data-stu-id="3708f-140">Once you leave this page the password will not be displayed again.</span></span>
> 

<span data-ttu-id="3708f-141">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span><span class="sxs-lookup"><span data-stu-id="3708f-141">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="3708f-142">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3708f-142">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the Azure portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="3708f-143">Provide the user name and password when prompted.</span><span class="sxs-lookup"><span data-stu-id="3708f-143">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="3708f-144">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="3708f-144">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="3708f-145">If this provides an error, try URL encoding the password portion of the command.</span><span class="sxs-lookup"><span data-stu-id="3708f-145">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="3708f-146">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span><span class="sxs-lookup"><span data-stu-id="3708f-146">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="3708f-147">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="3708f-147">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from the Azure portal")
```

<span data-ttu-id="3708f-148">Use the encoded password along with your user name and repository location to construct the git command.</span><span class="sxs-lookup"><span data-stu-id="3708f-148">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="3708f-149">Once the repository is cloned, you can view and work with it in your local file system.</span><span class="sxs-lookup"><span data-stu-id="3708f-149">Once the repository is cloned, you can view and work with it in your local file system.</span></span> <span data-ttu-id="3708f-150">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="3708f-150">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="3708f-151">To update your local repository with the most current service instance configuration</span><span class="sxs-lookup"><span data-stu-id="3708f-151">To update your local repository with the most current service instance configuration</span></span>

<span data-ttu-id="3708f-152">If you make changes to your API Management service instance in the Azure portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span><span class="sxs-lookup"><span data-stu-id="3708f-152">If you make changes to your API Management service instance in the Azure portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="3708f-153">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the Azure portal, and then issue the following command in your local repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-153">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the Azure portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="3708f-154">Before running `git pull` ensure that you are in the folder for your local repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-154">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="3708f-155">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span><span class="sxs-lookup"><span data-stu-id="3708f-155">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="3708f-156">To push changes from your local repo to the server repo</span><span class="sxs-lookup"><span data-stu-id="3708f-156">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="3708f-157">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span><span class="sxs-lookup"><span data-stu-id="3708f-157">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="3708f-158">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span><span class="sxs-lookup"><span data-stu-id="3708f-158">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="3708f-159">To push all of the commits to the server, run the following command.</span><span class="sxs-lookup"><span data-stu-id="3708f-159">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="3708f-160">To deploy any service configuration changes to the API Management service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-160">To deploy any service configuration changes to the API Management service instance</span></span>

<span data-ttu-id="3708f-161">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-161">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

<span data-ttu-id="3708f-162">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="3708f-162">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="3708f-163">File and folder structure reference of local Git repository</span><span class="sxs-lookup"><span data-stu-id="3708f-163">File and folder structure reference of local Git repository</span></span>

<span data-ttu-id="3708f-164">The files and folders in the local git repository contain the configuration information about the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-164">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="3708f-165">Item</span><span class="sxs-lookup"><span data-stu-id="3708f-165">Item</span></span> | <span data-ttu-id="3708f-166">Description</span><span class="sxs-lookup"><span data-stu-id="3708f-166">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3708f-167">root api-management folder</span><span class="sxs-lookup"><span data-stu-id="3708f-167">root api-management folder</span></span> |<span data-ttu-id="3708f-168">Contains top-level configuration for the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-168">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="3708f-169">apis folder</span><span class="sxs-lookup"><span data-stu-id="3708f-169">apis folder</span></span> |<span data-ttu-id="3708f-170">Contains the configuration for the apis in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-170">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="3708f-171">groups folder</span><span class="sxs-lookup"><span data-stu-id="3708f-171">groups folder</span></span> |<span data-ttu-id="3708f-172">Contains the configuration for the groups in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-172">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="3708f-173">policies folder</span><span class="sxs-lookup"><span data-stu-id="3708f-173">policies folder</span></span> |<span data-ttu-id="3708f-174">Contains the policies in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-174">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="3708f-175">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="3708f-175">portalStyles folder</span></span> |<span data-ttu-id="3708f-176">Contains the configuration for the developer portal customizations in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-176">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="3708f-177">products folder</span><span class="sxs-lookup"><span data-stu-id="3708f-177">products folder</span></span> |<span data-ttu-id="3708f-178">Contains the configuration for the products in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-178">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="3708f-179">templates folder</span><span class="sxs-lookup"><span data-stu-id="3708f-179">templates folder</span></span> |<span data-ttu-id="3708f-180">Contains the configuration for the email templates in the service instance</span><span class="sxs-lookup"><span data-stu-id="3708f-180">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="3708f-181">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span><span class="sxs-lookup"><span data-stu-id="3708f-181">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="3708f-182">The files within each folder are specific for the entity type described by the folder name.</span><span class="sxs-lookup"><span data-stu-id="3708f-182">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="3708f-183">File type</span><span class="sxs-lookup"><span data-stu-id="3708f-183">File type</span></span> | <span data-ttu-id="3708f-184">Purpose</span><span class="sxs-lookup"><span data-stu-id="3708f-184">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="3708f-185">json</span><span class="sxs-lookup"><span data-stu-id="3708f-185">json</span></span> |<span data-ttu-id="3708f-186">Configuration information about the respective entity</span><span class="sxs-lookup"><span data-stu-id="3708f-186">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="3708f-187">html</span><span class="sxs-lookup"><span data-stu-id="3708f-187">html</span></span> |<span data-ttu-id="3708f-188">Descriptions about the entity, often displayed in the developer portal</span><span class="sxs-lookup"><span data-stu-id="3708f-188">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="3708f-189">xml</span><span class="sxs-lookup"><span data-stu-id="3708f-189">xml</span></span> |<span data-ttu-id="3708f-190">Policy statements</span><span class="sxs-lookup"><span data-stu-id="3708f-190">Policy statements</span></span> |
| <span data-ttu-id="3708f-191">css</span><span class="sxs-lookup"><span data-stu-id="3708f-191">css</span></span> |<span data-ttu-id="3708f-192">Style sheets for developer portal customization</span><span class="sxs-lookup"><span data-stu-id="3708f-192">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="3708f-193">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-193">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="3708f-194">The following entities are not contained in the Git repository and cannot be configured using Git.</span><span class="sxs-lookup"><span data-stu-id="3708f-194">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="3708f-195">Users</span><span class="sxs-lookup"><span data-stu-id="3708f-195">Users</span></span>
> * <span data-ttu-id="3708f-196">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="3708f-196">Subscriptions</span></span>
> * <span data-ttu-id="3708f-197">Properties</span><span class="sxs-lookup"><span data-stu-id="3708f-197">Properties</span></span>
> * <span data-ttu-id="3708f-198">Developer portal entities other than styles</span><span class="sxs-lookup"><span data-stu-id="3708f-198">Developer portal entities other than styles</span></span>
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="3708f-199">Root api-management folder</span><span class="sxs-lookup"><span data-stu-id="3708f-199">Root api-management folder</span></span>
<span data-ttu-id="3708f-200">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span><span class="sxs-lookup"><span data-stu-id="3708f-200">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="3708f-201">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="3708f-201">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="3708f-202">Identity setting</span><span class="sxs-lookup"><span data-stu-id="3708f-202">Identity setting</span></span> | <span data-ttu-id="3708f-203">Maps to</span><span class="sxs-lookup"><span data-stu-id="3708f-203">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="3708f-204">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="3708f-204">RegistrationEnabled</span></span> |<span data-ttu-id="3708f-205">**Redirect anonymous users to sign-in page** checkbox</span><span class="sxs-lookup"><span data-stu-id="3708f-205">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="3708f-206">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="3708f-206">UserRegistrationTerms</span></span> |<span data-ttu-id="3708f-207">**Terms of use on user signup** textbox</span><span class="sxs-lookup"><span data-stu-id="3708f-207">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="3708f-208">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="3708f-208">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="3708f-209">**Show terms of use on signup page** checkbox</span><span class="sxs-lookup"><span data-stu-id="3708f-209">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="3708f-210">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="3708f-210">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="3708f-211">**Require consent** checkbox</span><span class="sxs-lookup"><span data-stu-id="3708f-211">**Require consent** checkbox</span></span> |

<span data-ttu-id="3708f-212">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="3708f-212">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="3708f-213">Delegation setting</span><span class="sxs-lookup"><span data-stu-id="3708f-213">Delegation setting</span></span> | <span data-ttu-id="3708f-214">Maps to</span><span class="sxs-lookup"><span data-stu-id="3708f-214">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="3708f-215">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="3708f-215">DelegationEnabled</span></span> |<span data-ttu-id="3708f-216">**Delegate sign-in & sign-up** checkbox</span><span class="sxs-lookup"><span data-stu-id="3708f-216">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="3708f-217">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="3708f-217">DelegationUrl</span></span> |<span data-ttu-id="3708f-218">**Delegation endpoint URL** textbox</span><span class="sxs-lookup"><span data-stu-id="3708f-218">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="3708f-219">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="3708f-219">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="3708f-220">**Delegate product subscription** checkbox</span><span class="sxs-lookup"><span data-stu-id="3708f-220">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="3708f-221">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="3708f-221">DelegationValidationKey</span></span> |<span data-ttu-id="3708f-222">**Delegate Validation Key** textbox</span><span class="sxs-lookup"><span data-stu-id="3708f-222">**Delegate Validation Key** textbox</span></span> |

<span data-ttu-id="3708f-223">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-223">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="3708f-224">apis folder</span><span class="sxs-lookup"><span data-stu-id="3708f-224">apis folder</span></span>
<span data-ttu-id="3708f-225">The `apis` folder contains a folder for each API in the service instance, which contains the following items.</span><span class="sxs-lookup"><span data-stu-id="3708f-225">The `apis` folder contains a folder for each API in the service instance, which contains the following items.</span></span>

* <span data-ttu-id="3708f-226">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span><span class="sxs-lookup"><span data-stu-id="3708f-226">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="3708f-227">This is the same information that would be returned if you were to call [Get a specific API](https://docs.microsoft.com/en-us/rest/api/apimanagement/api/get) with `export=true` in `application/json` format.</span><span class="sxs-lookup"><span data-stu-id="3708f-227">This is the same information that would be returned if you were to call [Get a specific API](https://docs.microsoft.com/en-us/rest/api/apimanagement/api/get) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="3708f-228">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://docs.microsoft.com/en-us/java/api/com.microsoft.azure.storage.table._entity_property).</span><span class="sxs-lookup"><span data-stu-id="3708f-228">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://docs.microsoft.com/en-us/java/api/com.microsoft.azure.storage.table._entity_property).</span></span>
* <span data-ttu-id="3708f-229">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span><span class="sxs-lookup"><span data-stu-id="3708f-229">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="3708f-230">Each file contains the description of a single operation in the API, which maps to the `description` property of the [operation entity](https://docs.microsoft.com/en-us/rest/api/visualstudio/operations/list#operationproperties) in the REST API.</span><span class="sxs-lookup"><span data-stu-id="3708f-230">Each file contains the description of a single operation in the API, which maps to the `description` property of the [operation entity](https://docs.microsoft.com/en-us/rest/api/visualstudio/operations/list#operationproperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="3708f-231">groups folder</span><span class="sxs-lookup"><span data-stu-id="3708f-231">groups folder</span></span>
<span data-ttu-id="3708f-232">The `groups` folder contains a folder for each group defined in the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-232">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="3708f-233">`groups\<group name>\configuration.json` - this is the configuration for the group.</span><span class="sxs-lookup"><span data-stu-id="3708f-233">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="3708f-234">This is the same information that would be returned if you were to call the [Get a specific group](https://docs.microsoft.com/en-us/rest/api/apimanagement/group/get) operation.</span><span class="sxs-lookup"><span data-stu-id="3708f-234">This is the same information that would be returned if you were to call the [Get a specific group](https://docs.microsoft.com/en-us/rest/api/apimanagement/group/get) operation.</span></span>
* <span data-ttu-id="3708f-235">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity).</span><span class="sxs-lookup"><span data-stu-id="3708f-235">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-group-entity).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="3708f-236">policies folder</span><span class="sxs-lookup"><span data-stu-id="3708f-236">policies folder</span></span>
<span data-ttu-id="3708f-237">The `policies` folder contains the policy statements for your service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-237">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="3708f-238">`policies\global.xml` - contains policies defined at global scope for your service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-238">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="3708f-239">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span><span class="sxs-lookup"><span data-stu-id="3708f-239">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="3708f-240">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span><span class="sxs-lookup"><span data-stu-id="3708f-240">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="3708f-241">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span><span class="sxs-lookup"><span data-stu-id="3708f-241">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="3708f-242">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="3708f-242">portalStyles folder</span></span>
<span data-ttu-id="3708f-243">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-243">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="3708f-244">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span><span class="sxs-lookup"><span data-stu-id="3708f-244">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="3708f-245">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span><span class="sxs-lookup"><span data-stu-id="3708f-245">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="3708f-246">products folder</span><span class="sxs-lookup"><span data-stu-id="3708f-246">products folder</span></span>
<span data-ttu-id="3708f-247">The `products` folder contains a folder for each product defined in the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-247">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="3708f-248">`products\<product name>\configuration.json` - this is the configuration for the product.</span><span class="sxs-lookup"><span data-stu-id="3708f-248">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="3708f-249">This is the same information that would be returned if you were to call the [Get a specific product](https://docs.microsoft.com/en-us/rest/api/apimanagement/product/get) operation.</span><span class="sxs-lookup"><span data-stu-id="3708f-249">This is the same information that would be returned if you were to call the [Get a specific product](https://docs.microsoft.com/en-us/rest/api/apimanagement/product/get) operation.</span></span>
* <span data-ttu-id="3708f-250">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-product-entity) in the REST API.</span><span class="sxs-lookup"><span data-stu-id="3708f-250">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-product-entity) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="3708f-251">templates</span><span class="sxs-lookup"><span data-stu-id="3708f-251">templates</span></span>
<span data-ttu-id="3708f-252">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span><span class="sxs-lookup"><span data-stu-id="3708f-252">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="3708f-253">`<template name>\configuration.json` - this is the configuration for the email template.</span><span class="sxs-lookup"><span data-stu-id="3708f-253">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="3708f-254">`<template name>\body.html` - this is the body of the email template.</span><span class="sxs-lookup"><span data-stu-id="3708f-254">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3708f-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="3708f-255">Next steps</span></span>
<span data-ttu-id="3708f-256">For information on other ways to manage your service instance, see:</span><span class="sxs-lookup"><span data-stu-id="3708f-256">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="3708f-257">Manage your service instance using the following PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="3708f-257">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="3708f-258">Service deployment PowerShell cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="3708f-258">Service deployment PowerShell cmdlet reference</span></span>](https://docs.microsoft.com/powershell/module/wds)
  * [<span data-ttu-id="3708f-259">Service management PowerShell cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="3708f-259">Service management PowerShell cmdlet reference</span></span>](https://docs.microsoft.com/powershell/azure/servicemanagement/overview)
* <span data-ttu-id="3708f-260">Manage your service instance using the REST API</span><span class="sxs-lookup"><span data-stu-id="3708f-260">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="3708f-261">API Management REST API reference</span><span class="sxs-lookup"><span data-stu-id="3708f-261">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)


[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




