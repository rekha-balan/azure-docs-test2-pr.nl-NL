---
title: Continuous delivery for cloud services with Visual Studio Online | Microsoft Docs
description: Learn how to set up continuous delivery for Azure cloud apps without saving diagnostics storage key to the service configuration files
services: cloud-services
documentationcenter: ''
author: cawa
manager: paulyuk
editor: ''
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 1167f02e2b7fbab1694bbb3062ff24259e0c5e05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660547"
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="1b8d7-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="1b8d7-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="1b8d7-104">It is a common practice to open source projects nowadays.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="1b8d7-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="1b8d7-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="1b8d7-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="1b8d7-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span><span class="sxs-lookup"><span data-stu-id="1b8d7-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="1b8d7-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="1b8d7-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="1b8d7-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="1b8d7-112">The following steps describe how the new Cloud Services tooling works:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="1b8d7-113">1. Open the Role designer</span><span class="sxs-lookup"><span data-stu-id="1b8d7-113">1. Open the Role designer</span></span>
* <span data-ttu-id="1b8d7-114">Double click or right click on a Cloud Services role to open Role designer</span><span class="sxs-lookup"><span data-stu-id="1b8d7-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Open role designer][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="1b8d7-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span><span class="sxs-lookup"><span data-stu-id="1b8d7-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="1b8d7-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![Local storage emulator connection string is not secret][1]

* <span data-ttu-id="1b8d7-119">If you are creating a new project, by default this checkbox is unchecked.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="1b8d7-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="1b8d7-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="1b8d7-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="1b8d7-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![Storage key is saved under user profile folder][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="1b8d7-124">3. Select a diagnostics storage account</span><span class="sxs-lookup"><span data-stu-id="1b8d7-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="1b8d7-125">Select a storage account from the dialog launched by clicking the “…”</span><span class="sxs-lookup"><span data-stu-id="1b8d7-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="1b8d7-126">button.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-126">button.</span></span> <span data-ttu-id="1b8d7-127">Notice how the storage connection string generated will not have the storage account key.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="1b8d7-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="1b8d7-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="1b8d7-129">4.    Debugging the project</span><span class="sxs-lookup"><span data-stu-id="1b8d7-129">4.    Debugging the project</span></span>
* <span data-ttu-id="1b8d7-130">F5 to start debugging in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="1b8d7-131">Everything should work in the same way as before.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="1b8d7-132">![Start debugging locally][3]</span><span class="sxs-lookup"><span data-stu-id="1b8d7-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="1b8d7-133">5. Publish project from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b8d7-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="1b8d7-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="1b8d7-135">6. Additional information</span><span class="sxs-lookup"><span data-stu-id="1b8d7-135">6. Additional information</span></span>
> <span data-ttu-id="1b8d7-136">Note: The Settings panel in the role designer will stay as it is for now.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="1b8d7-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Add settings][4]

> <span data-ttu-id="1b8d7-139">Note: If enabled, the Application Insights key will be stored as plain text.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="1b8d7-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="1b8d7-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span><span class="sxs-lookup"><span data-stu-id="1b8d7-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="1b8d7-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="1b8d7-143">1.    Obtain a VSO account</span><span class="sxs-lookup"><span data-stu-id="1b8d7-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="1b8d7-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span><span class="sxs-lookup"><span data-stu-id="1b8d7-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="1b8d7-145">[Create team project][Create team project] in your Visual Studio online account</span><span class="sxs-lookup"><span data-stu-id="1b8d7-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="1b8d7-146">2.    Setup source control in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b8d7-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="1b8d7-147">Connect to a team project</span><span class="sxs-lookup"><span data-stu-id="1b8d7-147">Connect to a team project</span></span>

![Connect to team project][5]

![Select team project to connect to][6]

* <span data-ttu-id="1b8d7-150">Add your project to source control</span><span class="sxs-lookup"><span data-stu-id="1b8d7-150">Add your project to source control</span></span>

![Add project to source control][7]

![Map project to a source control folder][8]

* <span data-ttu-id="1b8d7-153">Check in your project from Team Explorer</span><span class="sxs-lookup"><span data-stu-id="1b8d7-153">Check in your project from Team Explorer</span></span>

![Check in project to source control][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="1b8d7-155">3.    Configure Build process</span><span class="sxs-lookup"><span data-stu-id="1b8d7-155">3.    Configure Build process</span></span>
* <span data-ttu-id="1b8d7-156">Browse to your team project and add a new build process Templates</span><span class="sxs-lookup"><span data-stu-id="1b8d7-156">Browse to your team project and add a new build process Templates</span></span>

![Add a new build][10]

* <span data-ttu-id="1b8d7-158">Select build task</span><span class="sxs-lookup"><span data-stu-id="1b8d7-158">Select build task</span></span>

![Add a build task][11]

![Select Visual Studio Build task template][12]

* <span data-ttu-id="1b8d7-161">Edit build task input.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-161">Edit build task input.</span></span> <span data-ttu-id="1b8d7-162">Please customize the build parameters according to your need</span><span class="sxs-lookup"><span data-stu-id="1b8d7-162">Please customize the build parameters according to your need</span></span>

![Configure build task][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="1b8d7-164">Configure build variables</span><span class="sxs-lookup"><span data-stu-id="1b8d7-164">Configure build variables</span></span>

![Configure build variables][14]

* <span data-ttu-id="1b8d7-166">Add a task to upload build drop</span><span class="sxs-lookup"><span data-stu-id="1b8d7-166">Add a task to upload build drop</span></span>

![Choose publish build drop task][15]

![Configure publish build drop task][16]

* <span data-ttu-id="1b8d7-169">Run the build</span><span class="sxs-lookup"><span data-stu-id="1b8d7-169">Run the build</span></span>

![Queue New Build][17]

![View build summary][18]

* <span data-ttu-id="1b8d7-172">if the build is successful you will see a result similar to below</span><span class="sxs-lookup"><span data-stu-id="1b8d7-172">if the build is successful you will see a result similar to below</span></span>

![Build result][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="1b8d7-174">4.    Configure Release process</span><span class="sxs-lookup"><span data-stu-id="1b8d7-174">4.    Configure Release process</span></span>
* <span data-ttu-id="1b8d7-175">Create a new release</span><span class="sxs-lookup"><span data-stu-id="1b8d7-175">Create a new release</span></span>

![Create new release][20]

* <span data-ttu-id="1b8d7-177">Select the Azure Cloud Services Deployment task</span><span class="sxs-lookup"><span data-stu-id="1b8d7-177">Select the Azure Cloud Services Deployment task</span></span>

![Select Azure Cloud Services deployment task][21]

* <span data-ttu-id="1b8d7-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="1b8d7-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="1b8d7-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="1b8d7-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span><span class="sxs-lookup"><span data-stu-id="1b8d7-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Configure Cloud Services deployment task][22]

* <span data-ttu-id="1b8d7-184">Use secret build variables to save storage Keys.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="1b8d7-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span><span class="sxs-lookup"><span data-stu-id="1b8d7-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Save storage keys in secret build variables][23]

* <span data-ttu-id="1b8d7-187">Create a release and deploy your project to Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-187">Create a release and deploy your project to Azure</span></span>

![Create new release][24]

## <a name="next-steps"></a><span data-ttu-id="1b8d7-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b8d7-189">Next steps</span></span>
<span data-ttu-id="1b8d7-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="1b8d7-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-01.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-02.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/file-01.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-06.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-07.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-08.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vs-09.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-01.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-02.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-03.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-04.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-05.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-06.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-07.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-08.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-09.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-10.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-11.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-12.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-13.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-14.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-vs-ci/vso-15.png

























