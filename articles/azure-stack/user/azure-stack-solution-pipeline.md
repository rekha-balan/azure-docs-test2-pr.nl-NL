---
title: Deploy your app to Azure and Azure Stack | Microsoft Docs
description: Learn how to deploy apps to Azure and Azure Stack with a hybrid CI/CD pipeline.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/04/2018
ms.author: mabrigg
ms.reviewer: Anjay.Ajodha
ms.openlocfilehash: 773acd3a22244403548ef4ce35164291f5c0be7d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869093"
---
# <a name="tutorial-deploy-apps-to-azure-and-azure-stack"></a><span data-ttu-id="c7c9b-103">Tutorial: deploy apps to Azure and Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c7c9b-103">Tutorial: deploy apps to Azure and Azure Stack</span></span>

<span data-ttu-id="c7c9b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="c7c9b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="c7c9b-105">Learn how to deploy an application to Azure and Azure Stack using a hybrid continuous integration/continuous delivery (CI/CD) pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-105">Learn how to deploy an application to Azure and Azure Stack using a hybrid continuous integration/continuous delivery (CI/CD) pipeline.</span></span>

<span data-ttu-id="c7c9b-106">In this tutorial, you'll create a sample environment to:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-106">In this tutorial, you'll create a sample environment to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7c9b-107">Initiate a new build based on code commits to your Azure DevOps Services repository.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-107">Initiate a new build based on code commits to your Azure DevOps Services repository.</span></span>
> * <span data-ttu-id="c7c9b-108">Automatically deploy your app to global Azure for user acceptance testing.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-108">Automatically deploy your app to global Azure for user acceptance testing.</span></span>
> * <span data-ttu-id="c7c9b-109">When your code passes testing, automatically deploy the app to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-109">When your code passes testing, automatically deploy the app to Azure Stack.</span></span>

## <a name="benefits-of-the-hybrid-delivery-build-pipe"></a><span data-ttu-id="c7c9b-110">Benefits of the hybrid delivery build pipe</span><span class="sxs-lookup"><span data-stu-id="c7c9b-110">Benefits of the hybrid delivery build pipe</span></span>

<span data-ttu-id="c7c9b-111">Continuity, security, and reliability are key elements of application deployment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-111">Continuity, security, and reliability are key elements of application deployment.</span></span> <span data-ttu-id="c7c9b-112">These elements are essential to your organization and critical to your development team.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-112">These elements are essential to your organization and critical to your development team.</span></span> <span data-ttu-id="c7c9b-113">A hybrid CI/CD pipeline enables you to consolidate your build pipes across your on-premises environment and the public cloud.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-113">A hybrid CI/CD pipeline enables you to consolidate your build pipes across your on-premises environment and the public cloud.</span></span> <span data-ttu-id="c7c9b-114">A hybrid delivery model also lets you change deployment locations without changing your application.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-114">A hybrid delivery model also lets you change deployment locations without changing your application.</span></span>

<span data-ttu-id="c7c9b-115">Other benefits to using the hybrid approach are:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-115">Other benefits to using the hybrid approach are:</span></span>

* <span data-ttu-id="c7c9b-116">You can maintain a consistent set of development tools across your on-premises Azure Stack environment and the Azure public cloud.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-116">You can maintain a consistent set of development tools across your on-premises Azure Stack environment and the Azure public cloud.</span></span>  <span data-ttu-id="c7c9b-117">A common tool set makes it easier to implement CI/CD patterns and practices.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-117">A common tool set makes it easier to implement CI/CD patterns and practices.</span></span>
* <span data-ttu-id="c7c9b-118">Apps and services deployed in Azure or Azure Stack are interchangeable and the same code can run in either location.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-118">Apps and services deployed in Azure or Azure Stack are interchangeable and the same code can run in either location.</span></span> <span data-ttu-id="c7c9b-119">You can take advantage of on-premises and public cloud features and capabilities.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-119">You can take advantage of on-premises and public cloud features and capabilities.</span></span>

<span data-ttu-id="c7c9b-120">To learn more about CI and CD:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-120">To learn more about CI and CD:</span></span>

* [<span data-ttu-id="c7c9b-121">What is Continuous Integration?</span><span class="sxs-lookup"><span data-stu-id="c7c9b-121">What is Continuous Integration?</span></span>](https://www.visualstudio.com/learn/what-is-continuous-integration/)
* [<span data-ttu-id="c7c9b-122">What is Continuous Delivery?</span><span class="sxs-lookup"><span data-stu-id="c7c9b-122">What is Continuous Delivery?</span></span>](https://www.visualstudio.com/learn/what-is-continuous-delivery/)

## <a name="prerequisites"></a><span data-ttu-id="c7c9b-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7c9b-123">Prerequisites</span></span>

<span data-ttu-id="c7c9b-124">You need to have components in place to build a hybrid CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-124">You need to have components in place to build a hybrid CI/CD pipeline.</span></span> <span data-ttu-id="c7c9b-125">The following components will take time to prepare:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-125">The following components will take time to prepare:</span></span>

* <span data-ttu-id="c7c9b-126">An Azure OEM/hardware partner can deploy a production Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-126">An Azure OEM/hardware partner can deploy a production Azure Stack.</span></span> <span data-ttu-id="c7c9b-127">All users can deploy the Azure Stack Development Kit (ASDK).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-127">All users can deploy the Azure Stack Development Kit (ASDK).</span></span>
* <span data-ttu-id="c7c9b-128">An Azure Stack Operator must also: deploy the App Service, create plans and offers, create a tenant subscription, and add the Windows Server 2016 image.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-128">An Azure Stack Operator must also: deploy the App Service, create plans and offers, create a tenant subscription, and add the Windows Server 2016 image.</span></span>

>[!NOTE]
><span data-ttu-id="c7c9b-129">If you already have some of these components deployed, make sure they meet the all the requirements before you start this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-129">If you already have some of these components deployed, make sure they meet the all the requirements before you start this tutorial.</span></span>

<span data-ttu-id="c7c9b-130">This tutorial assumes that you have some basic knowledge of Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-130">This tutorial assumes that you have some basic knowledge of Azure and Azure Stack.</span></span> <span data-ttu-id="c7c9b-131">To learn more before starting the tutorial, read the following articles:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-131">To learn more before starting the tutorial, read the following articles:</span></span>

* [<span data-ttu-id="c7c9b-132">Introduction to Azure</span><span class="sxs-lookup"><span data-stu-id="c7c9b-132">Introduction to Azure</span></span>](https://azure.microsoft.com/overview/what-is-azure/)
* [<span data-ttu-id="c7c9b-133">Azure Stack Key Concepts</span><span class="sxs-lookup"><span data-stu-id="c7c9b-133">Azure Stack Key Concepts</span></span>](https://docs.microsoft.com/azure/azure-stack/azure-stack-key-features)

### <a name="azure-requirements"></a><span data-ttu-id="c7c9b-134">Azure requirements</span><span class="sxs-lookup"><span data-stu-id="c7c9b-134">Azure requirements</span></span>

* <span data-ttu-id="c7c9b-135">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-135">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
* <span data-ttu-id="c7c9b-136">Create a [Web App](https://docs.microsoft.com/azure/app-service/app-service-web-overview) in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-136">Create a [Web App](https://docs.microsoft.com/azure/app-service/app-service-web-overview) in Azure.</span></span> <span data-ttu-id="c7c9b-137">Make note of the Web App URL, you need to use it in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-137">Make note of the Web App URL, you need to use it in the tutorial.</span></span>

### <a name="azure-stack-requirements"></a><span data-ttu-id="c7c9b-138">Azure Stack requirements</span><span class="sxs-lookup"><span data-stu-id="c7c9b-138">Azure Stack requirements</span></span>

* <span data-ttu-id="c7c9b-139">Use an Azure Stack integrated system or deploy the Azure Stack Development Kit (ASDK).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-139">Use an Azure Stack integrated system or deploy the Azure Stack Development Kit (ASDK).</span></span> <span data-ttu-id="c7c9b-140">To deploy the ASDK:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-140">To deploy the ASDK:</span></span>
    * <span data-ttu-id="c7c9b-141">The [Tutorial: deploy the ASDK using the installer](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy) gives detailed deployment instructions.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-141">The [Tutorial: deploy the ASDK using the installer](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy) gives detailed deployment instructions.</span></span>
    * <span data-ttu-id="c7c9b-142">Use the [ConfigASDK.ps1](https://github.com/mattmcspirit/azurestack/blob/master/deployment/ConfigASDK.ps1 ) PowerShell script to automate ASDK post-deployment steps.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-142">Use the [ConfigASDK.ps1](https://github.com/mattmcspirit/azurestack/blob/master/deployment/ConfigASDK.ps1 ) PowerShell script to automate ASDK post-deployment steps.</span></span>

    > [!Note]
    > <span data-ttu-id="c7c9b-143">The ASDK installation takes approximately seven hours to complete, so plan accordingly.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-143">The ASDK installation takes approximately seven hours to complete, so plan accordingly.</span></span>

 * <span data-ttu-id="c7c9b-144">Deploy [App Service](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-deploy) PaaS services to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-144">Deploy [App Service](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-deploy) PaaS services to Azure Stack.</span></span>
 * <span data-ttu-id="c7c9b-145">Create [Plan/Offers](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview) in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-145">Create [Plan/Offers](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview) in Azure Stack.</span></span>
 * <span data-ttu-id="c7c9b-146">Create a [tenant subscription](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm) in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-146">Create a [tenant subscription](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm) in Azure Stack.</span></span>
 * <span data-ttu-id="c7c9b-147">Create a Web App in the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-147">Create a Web App in the tenant subscription.</span></span> <span data-ttu-id="c7c9b-148">Make note of the new Web App URL for later use.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-148">Make note of the new Web App URL for later use.</span></span>
 * <span data-ttu-id="c7c9b-149">Deploy Azure DevOps Services Virtual Machine in the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-149">Deploy Azure DevOps Services Virtual Machine in the tenant subscription.</span></span>
* <span data-ttu-id="c7c9b-150">Provide a Windows Server 2016 image with .NET 3.5 for a virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-150">Provide a Windows Server 2016 image with .NET 3.5 for a virtual machine (VM).</span></span> <span data-ttu-id="c7c9b-151">This VM will be built on your Azure Stack as a private build agent.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-151">This VM will be built on your Azure Stack as a private build agent.</span></span>

### <a name="developer-tool-requirements"></a><span data-ttu-id="c7c9b-152">Developer tool requirements</span><span class="sxs-lookup"><span data-stu-id="c7c9b-152">Developer tool requirements</span></span>

* <span data-ttu-id="c7c9b-153">Create an [Azure DevOps Services workspace](https://docs.microsoft.com/azure/devops/repos/tfvc/create-work-workspaces).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-153">Create an [Azure DevOps Services workspace](https://docs.microsoft.com/azure/devops/repos/tfvc/create-work-workspaces).</span></span> <span data-ttu-id="c7c9b-154">The sign-up process creates a project named **MyFirstProject**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-154">The sign-up process creates a project named **MyFirstProject**.</span></span>
* <span data-ttu-id="c7c9b-155">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) and [sign-in to Azure DevOps Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-155">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) and [sign-in to Azure DevOps Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>
* <span data-ttu-id="c7c9b-156">Connect to your project and [clone it locally](https://www.visualstudio.com/docs/git/gitquickstart).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-156">Connect to your project and [clone it locally](https://www.visualstudio.com/docs/git/gitquickstart).</span></span>

 > [!Note]
 > <span data-ttu-id="c7c9b-157">Your Azure Stack environment needs the correct images syndicated to run Windows Server and SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-157">Your Azure Stack environment needs the correct images syndicated to run Windows Server and SQL Server.</span></span> <span data-ttu-id="c7c9b-158">It must also have App Service deployed.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-158">It must also have App Service deployed.</span></span>

## <a name="prepare-the-private-azure-pipelines-agent-for-azure-devops-services-integration"></a><span data-ttu-id="c7c9b-159">Prepare the private Azure Pipelines agent for Azure DevOps Services integration</span><span class="sxs-lookup"><span data-stu-id="c7c9b-159">Prepare the private Azure Pipelines agent for Azure DevOps Services integration</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c7c9b-160">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7c9b-160">Prerequisites</span></span>

<span data-ttu-id="c7c9b-161">Azure DevOps Services authenticates against Azure Resource Manager using a Service Principal.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-161">Azure DevOps Services authenticates against Azure Resource Manager using a Service Principal.</span></span> <span data-ttu-id="c7c9b-162">Azure DevOps Services must have the **Contributor** role to provision resources in an Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-162">Azure DevOps Services must have the **Contributor** role to provision resources in an Azure Stack subscription.</span></span>

<span data-ttu-id="c7c9b-163">The following steps describe what's required to configure authentication:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-163">The following steps describe what's required to configure authentication:</span></span>

1. <span data-ttu-id="c7c9b-164">Create a Service Principal, or use an existing Service Principal.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-164">Create a Service Principal, or use an existing Service Principal.</span></span>
2. <span data-ttu-id="c7c9b-165">Create Authentication keys for the Service Principal.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-165">Create Authentication keys for the Service Principal.</span></span>
3. <span data-ttu-id="c7c9b-166">Validate the Azure Stack Subscription via Role-Based Access Control to allow the Service Principal Name (SPN) to be part of the Contributor’s role.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-166">Validate the Azure Stack Subscription via Role-Based Access Control to allow the Service Principal Name (SPN) to be part of the Contributor’s role.</span></span>
4. <span data-ttu-id="c7c9b-167">Create a new Service Definition in Azure DevOps Services using the Azure Stack endpoints and SPN information.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-167">Create a new Service Definition in Azure DevOps Services using the Azure Stack endpoints and SPN information.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="c7c9b-168">Create a Service Principal</span><span class="sxs-lookup"><span data-stu-id="c7c9b-168">Create a Service Principal</span></span>

<span data-ttu-id="c7c9b-169">Refer to the [Service Principal Creation](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) instructions to create a service principal.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-169">Refer to the [Service Principal Creation](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) instructions to create a service principal.</span></span> <span data-ttu-id="c7c9b-170">Choose **Web App/API** for the Application Type or [use the PowerShell script](https://github.com/Microsoft/vsts-rm-extensions/blob/master/TaskModules/powershell/Azure/SPNCreation.ps1#L5) as explained in the article [Create an Azure Resource Manager service connection with an existing service principal ](https://docs.microsoft.com/vsts/pipelines/library/connect-to-azure?view=vsts#create-an-azure-resource-manager-service-connection-with-an-existing-service-principal).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-170">Choose **Web App/API** for the Application Type or [use the PowerShell script](https://github.com/Microsoft/vsts-rm-extensions/blob/master/TaskModules/powershell/Azure/SPNCreation.ps1#L5) as explained in the article [Create an Azure Resource Manager service connection with an existing service principal ](https://docs.microsoft.com/vsts/pipelines/library/connect-to-azure?view=vsts#create-an-azure-resource-manager-service-connection-with-an-existing-service-principal).</span></span>

 > [!Note]  
 > <span data-ttu-id="c7c9b-171">If you use the script to create an Azure Stack Azure Resource Manager endpoint, you need to pass the **-azureStackManagementURL** parameter and **-environmentName** parameter.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-171">If you use the script to create an Azure Stack Azure Resource Manager endpoint, you need to pass the **-azureStackManagementURL** parameter and **-environmentName** parameter.</span></span> <span data-ttu-id="c7c9b-172">For example:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-172">For example:</span></span>  
> `-azureStackManagementURL https://management.local.azurestack.external -environmentName AzureStack`

### <a name="create-an-access-key"></a><span data-ttu-id="c7c9b-173">Create an access key</span><span class="sxs-lookup"><span data-stu-id="c7c9b-173">Create an access key</span></span>

<span data-ttu-id="c7c9b-174">A Service Principal requires a key for authentication.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-174">A Service Principal requires a key for authentication.</span></span> <span data-ttu-id="c7c9b-175">Use the following steps to generate a key.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-175">Use the following steps to generate a key.</span></span>

1. <span data-ttu-id="c7c9b-176">From **App registrations** in Azure Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-176">From **App registrations** in Azure Active Directory, select your application.</span></span>

    ![Select the application](media\azure-stack-solution-hybrid-pipeline\000_01.png)

2. <span data-ttu-id="c7c9b-178">Make note of the value of **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-178">Make note of the value of **Application ID**.</span></span> <span data-ttu-id="c7c9b-179">You will use that value when configuring the service endpoint in Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-179">You will use that value when configuring the service endpoint in Azure DevOps Services.</span></span>

    ![Application ID](media\azure-stack-solution-hybrid-pipeline\000_02.png)

3. <span data-ttu-id="c7c9b-181">To generate an authentication key, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-181">To generate an authentication key, select **Settings**.</span></span>

    ![Edit app settings](media\azure-stack-solution-hybrid-pipeline\000_03.png)

4. <span data-ttu-id="c7c9b-183">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-183">To generate an authentication key, select **Keys**.</span></span>

    ![Configure key settings](media\azure-stack-solution-hybrid-pipeline\000_04.png)

5. <span data-ttu-id="c7c9b-185">Provide a description for the key, and set the duration of the key.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-185">Provide a description for the key, and set the duration of the key.</span></span> <span data-ttu-id="c7c9b-186">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-186">When done, select **Save**.</span></span>

    ![Key description and duration](media\azure-stack-solution-hybrid-pipeline\000_05.png)

    <span data-ttu-id="c7c9b-188">After you save the key, the key **VALUE** is displayed.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-188">After you save the key, the key **VALUE** is displayed.</span></span> <span data-ttu-id="c7c9b-189">Copy this value because you can't get this value later.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-189">Copy this value because you can't get this value later.</span></span> <span data-ttu-id="c7c9b-190">You provide the **key value** with the application ID to sign in as the application.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-190">You provide the **key value** with the application ID to sign in as the application.</span></span> <span data-ttu-id="c7c9b-191">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-191">Store the key value where your application can retrieve it.</span></span>

    ![Key VALUE](media\azure-stack-solution-hybrid-pipeline\000_06.png)

### <a name="get-the-tenant-id"></a><span data-ttu-id="c7c9b-193">Get the tenant ID</span><span class="sxs-lookup"><span data-stu-id="c7c9b-193">Get the tenant ID</span></span>

<span data-ttu-id="c7c9b-194">As part of the service endpoint configuration, Azure DevOps Services requires the **Tenant ID** that corresponds to the AAD Directory that your Azure Stack stamp is deployed to.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-194">As part of the service endpoint configuration, Azure DevOps Services requires the **Tenant ID** that corresponds to the AAD Directory that your Azure Stack stamp is deployed to.</span></span> <span data-ttu-id="c7c9b-195">Use the following steps to get the Tenant ID.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-195">Use the following steps to get the Tenant ID.</span></span>

1. <span data-ttu-id="c7c9b-196">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-196">Select **Azure Active Directory**.</span></span>

    ![Azure Active Directory for tenant](media\azure-stack-solution-hybrid-pipeline\000_07.png)

2. <span data-ttu-id="c7c9b-198">To get the tenant ID, select **Properties** for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-198">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span>

    ![View tenant properties](media\azure-stack-solution-hybrid-pipeline\000_08.png)

3. <span data-ttu-id="c7c9b-200">Copy the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-200">Copy the **Directory ID**.</span></span> <span data-ttu-id="c7c9b-201">This value is your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-201">This value is your tenant ID.</span></span>

    ![Directory ID](media\azure-stack-solution-hybrid-pipeline\000_09.png)

### <a name="grant-the-service-principal-rights-to-deploy-resources-in-the-azure-stack-subscription"></a><span data-ttu-id="c7c9b-203">Grant the service principal rights to deploy resources in the Azure Stack subscription</span><span class="sxs-lookup"><span data-stu-id="c7c9b-203">Grant the service principal rights to deploy resources in the Azure Stack subscription</span></span>

<span data-ttu-id="c7c9b-204">To access resources in your subscription, you must assign the application to a role.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-204">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="c7c9b-205">Decide which role represents the best permissions for the application.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-205">Decide which role represents the best permissions for the application.</span></span> <span data-ttu-id="c7c9b-206">To learn about the available roles, see [RBAC: Built in Roles](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-206">To learn about the available roles, see [RBAC: Built in Roles](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).</span></span>

<span data-ttu-id="c7c9b-207">You can set the scope at the level of the subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-207">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="c7c9b-208">Permissions are inherited to lower levels of scope.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-208">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="c7c9b-209">For example, adding an application to the Reader role for a resource group means it can read the resource group and any of its resources.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-209">For example, adding an application to the Reader role for a resource group means it can read the resource group and any of its resources.</span></span>

1. <span data-ttu-id="c7c9b-210">Navigate to the level of scope you wish to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-210">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="c7c9b-211">For example, to assign a role at the subscription scope, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-211">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span>

    ![Select Subscriptions](media\azure-stack-solution-hybrid-pipeline\000_10.png)

2. <span data-ttu-id="c7c9b-213">In **Subscription**, select Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-213">In **Subscription**, select Visual Studio Enterprise.</span></span>

    ![Visual Studio Enterprise](media\azure-stack-solution-hybrid-pipeline\000_11.png)

3. <span data-ttu-id="c7c9b-215">In Visual Studio Enterprise, select **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-215">In Visual Studio Enterprise, select **Access Control (IAM)**.</span></span>

    ![Access Control (IAM)](media\azure-stack-solution-hybrid-pipeline\000_12.png)

4. <span data-ttu-id="c7c9b-217">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-217">Select **Add**.</span></span>

    ![Add](media\azure-stack-solution-hybrid-pipeline\000_13.png)

5. <span data-ttu-id="c7c9b-219">In **Add permissions**, select the role you that you want to assign to the application.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-219">In **Add permissions**, select the role you that you want to assign to the application.</span></span> <span data-ttu-id="c7c9b-220">In this example, the **Owner** role.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-220">In this example, the **Owner** role.</span></span>

    ![Owner role](media\azure-stack-solution-hybrid-pipeline\000_14.png)

6. <span data-ttu-id="c7c9b-222">By default, Azure Active Directory applications aren't displayed in the available options.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-222">By default, Azure Active Directory applications aren't displayed in the available options.</span></span> <span data-ttu-id="c7c9b-223">To find your application, you must provide its name in the **Select** field to search for it.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-223">To find your application, you must provide its name in the **Select** field to search for it.</span></span> <span data-ttu-id="c7c9b-224">Select the app.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-224">Select the app.</span></span>

    ![App search result](media\azure-stack-solution-hybrid-pipeline\000_16.png)

7. <span data-ttu-id="c7c9b-226">Select **Save** to finish assigning the role.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-226">Select **Save** to finish assigning the role.</span></span> <span data-ttu-id="c7c9b-227">You see your application in the list of users assigned to a role for that scope.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-227">You see your application in the list of users assigned to a role for that scope.</span></span>

### <a name="role-based-access-control"></a><span data-ttu-id="c7c9b-228">Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="c7c9b-228">Role-Based Access Control</span></span>

<span data-ttu-id="c7c9b-229">‎Azure Role-Based Access Control (RBAC) provides fine-grained access management for Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-229">‎Azure Role-Based Access Control (RBAC) provides fine-grained access management for Azure.</span></span> <span data-ttu-id="c7c9b-230">By using RBAC, you can control the level of access that users need to do their jobs.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-230">By using RBAC, you can control the level of access that users need to do their jobs.</span></span> <span data-ttu-id="c7c9b-231">For more information about Role-Based Access Control, see [Manage Access to Azure Subscription Resources](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal?toc=%252fazure%252factive-directory%252ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-231">For more information about Role-Based Access Control, see [Manage Access to Azure Subscription Resources](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal?toc=%252fazure%252factive-directory%252ftoc.json).</span></span>

### <a name="azure-devops-services-agent-pools"></a><span data-ttu-id="c7c9b-232">Azure DevOps Services Agent Pools</span><span class="sxs-lookup"><span data-stu-id="c7c9b-232">Azure DevOps Services Agent Pools</span></span>

<span data-ttu-id="c7c9b-233">Instead of managing each agent separately, you can organize agents into agent pools.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-233">Instead of managing each agent separately, you can organize agents into agent pools.</span></span> <span data-ttu-id="c7c9b-234">An agent pool defines the sharing boundary for all agents in that pool.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-234">An agent pool defines the sharing boundary for all agents in that pool.</span></span> <span data-ttu-id="c7c9b-235">In Azure DevOps Services, agent pools are scoped to the Azure DevOps Services organization, which means that you can share an agent pool across projects.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-235">In Azure DevOps Services, agent pools are scoped to the Azure DevOps Services organization, which means that you can share an agent pool across projects.</span></span> <span data-ttu-id="c7c9b-236">To learn more about agent pools, see [Create Agent Pools and Queues](https://docs.microsoft.com/azure/devops/pipelines/agents/pools-queues?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-236">To learn more about agent pools, see [Create Agent Pools and Queues](https://docs.microsoft.com/azure/devops/pipelines/agents/pools-queues?view=vsts).</span></span>

### <a name="add-a-personal-access-token-pat-for-azure-stack"></a><span data-ttu-id="c7c9b-237">Add a Personal Access Token (PAT) for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c7c9b-237">Add a Personal Access Token (PAT) for Azure Stack</span></span>

<span data-ttu-id="c7c9b-238">Create a Personal Access Token to access Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-238">Create a Personal Access Token to access Azure DevOps Services.</span></span>

1. <span data-ttu-id="c7c9b-239">Sign in to your Azure DevOps Services organization and select your organization profile name.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-239">Sign in to your Azure DevOps Services organization and select your organization profile name.</span></span>

2. <span data-ttu-id="c7c9b-240">Select **Manage Security** to access token creation page.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-240">Select **Manage Security** to access token creation page.</span></span>

    ![User sign-in](media\azure-stack-solution-hybrid-pipeline\000_17.png)

    ![Select a project](media\azure-stack-solution-hybrid-pipeline\000_18.png)

    ![Add Personal access token](media\azure-stack-solution-hybrid-pipeline\000_18a.png)

    ![Create token](media\azure-stack-solution-hybrid-pipeline\000_18b.png)

3. <span data-ttu-id="c7c9b-245">Copy the token.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-245">Copy the token.</span></span>

    > [!Note]
    > <span data-ttu-id="c7c9b-246">Save the token information.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-246">Save the token information.</span></span> <span data-ttu-id="c7c9b-247">This information isn't stored and won't be shown again when you leave the web page.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-247">This information isn't stored and won't be shown again when you leave the web page.</span></span>

    ![Personal access token](media\azure-stack-solution-hybrid-pipeline\000_19.png)

### <a name="install-the-azure-devops-services-build-agent-on-the-azure-stack-hosted-build-server"></a><span data-ttu-id="c7c9b-249">Install the Azure DevOps Services build agent on the Azure Stack hosted Build Server</span><span class="sxs-lookup"><span data-stu-id="c7c9b-249">Install the Azure DevOps Services build agent on the Azure Stack hosted Build Server</span></span>

1. <span data-ttu-id="c7c9b-250">Connect to your Build Server that you deployed on the Azure Stack host.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-250">Connect to your Build Server that you deployed on the Azure Stack host.</span></span>
2. <span data-ttu-id="c7c9b-251">Download and Deploy the build agent as a service using your personal access token (PAT) and run as the VM Admin account.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-251">Download and Deploy the build agent as a service using your personal access token (PAT) and run as the VM Admin account.</span></span>

    ![Download build agent](media\azure-stack-solution-hybrid-pipeline\010_downloadagent.png)

3. <span data-ttu-id="c7c9b-253">Navigate to the folder for the extracted build agent.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-253">Navigate to the folder for the extracted build agent.</span></span> <span data-ttu-id="c7c9b-254">Run the **config.cmd** file from an elevated command prompt.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-254">Run the **config.cmd** file from an elevated command prompt.</span></span>

    ![Extracted build agent](media\azure-stack-solution-hybrid-pipeline\000_20.png)

    ![Register build agent](media\azure-stack-solution-hybrid-pipeline\000_21.png)

4. <span data-ttu-id="c7c9b-257">When the config.cmd finishes, the build agent folder is updated with additional files.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-257">When the config.cmd finishes, the build agent folder is updated with additional files.</span></span> <span data-ttu-id="c7c9b-258">The folder with the extracted contents should look like the following:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-258">The folder with the extracted contents should look like the following:</span></span>

    ![Build agent folder update](media\azure-stack-solution-hybrid-pipeline\009_token_file.png)

    <span data-ttu-id="c7c9b-260">You can see the agent in Azure DevOps Services folder.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-260">You can see the agent in Azure DevOps Services folder.</span></span>

## <a name="endpoint-creation-permissions"></a><span data-ttu-id="c7c9b-261">Endpoint creation permissions</span><span class="sxs-lookup"><span data-stu-id="c7c9b-261">Endpoint creation permissions</span></span>

<span data-ttu-id="c7c9b-262">By creating endpoints, a Visual Studio Online (VSTO) build can deploy Azure Service apps to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-262">By creating endpoints, a Visual Studio Online (VSTO) build can deploy Azure Service apps to Azure Stack.</span></span> <span data-ttu-id="c7c9b-263">Azure DevOps Services connects to the build agent, which connects to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-263">Azure DevOps Services connects to the build agent, which connects to Azure Stack.</span></span>

![NorthwindCloud sample app in VSTO](media\azure-stack-solution-hybrid-pipeline\012_securityendpoints.png)

1. <span data-ttu-id="c7c9b-265">Sign in to VSTO and navigate to the app settings page.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-265">Sign in to VSTO and navigate to the app settings page.</span></span>
2. <span data-ttu-id="c7c9b-266">On **Settings**, select **Security**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-266">On **Settings**, select **Security**.</span></span>
3. <span data-ttu-id="c7c9b-267">In **Azure DevOps Services Groups**, select **Endpoint Creators**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-267">In **Azure DevOps Services Groups**, select **Endpoint Creators**.</span></span>

    ![NorthwindCloud Endpoint Creators](media\azure-stack-solution-hybrid-pipeline\013_endpoint_creators.png)

4. <span data-ttu-id="c7c9b-269">On the **Members** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-269">On the **Members** tab, select **Add**.</span></span>

    ![Add a member](media\azure-stack-solution-hybrid-pipeline\014_members_tab.png)

5. <span data-ttu-id="c7c9b-271">In **Add users and groups**, enter a user name and select that user from the list of users.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-271">In **Add users and groups**, enter a user name and select that user from the list of users.</span></span>
6. <span data-ttu-id="c7c9b-272">Select **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-272">Select **Save changes**.</span></span>
7. <span data-ttu-id="c7c9b-273">In the **Azure DevOps Services Groups** list, select **Endpoint Administrators**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-273">In the **Azure DevOps Services Groups** list, select **Endpoint Administrators**.</span></span>

    ![NorthwindCloud Endpoint Administrators](media\azure-stack-solution-hybrid-pipeline\015_save_endpoint.png)

8. <span data-ttu-id="c7c9b-275">On the **Members** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-275">On the **Members** tab, select **Add**.</span></span>
9. <span data-ttu-id="c7c9b-276">In **Add users and groups**, enter a user name and select that user from the list of users.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-276">In **Add users and groups**, enter a user name and select that user from the list of users.</span></span>
10. <span data-ttu-id="c7c9b-277">Select **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-277">Select **Save changes**.</span></span>

<span data-ttu-id="c7c9b-278">Now that the endpoint information exists, the Azure DevOps Services to Azure Stack connection is ready to use.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-278">Now that the endpoint information exists, the Azure DevOps Services to Azure Stack connection is ready to use.</span></span> <span data-ttu-id="c7c9b-279">The build agent in Azure Stack gets instructions from Azure DevOps Services, and then the agent conveys endpoint information for communication with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-279">The build agent in Azure Stack gets instructions from Azure DevOps Services, and then the agent conveys endpoint information for communication with Azure Stack.</span></span>
## <a name="create-an-azure-stack-endpoint"></a><span data-ttu-id="c7c9b-280">Create an Azure Stack endpoint</span><span class="sxs-lookup"><span data-stu-id="c7c9b-280">Create an Azure Stack endpoint</span></span>

<span data-ttu-id="c7c9b-281">You can follow the instructions in [Create an Azure Resource Manager service connection with an existing service principal ](https://docs.microsoft.com/vsts/pipelines/library/connect-to-azure?view=vsts#create-an-azure-resource-manager-service-connection-with-an-existing-service-principal) article to create a service connection with an existing service principal and use the following mapping:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-281">You can follow the instructions in [Create an Azure Resource Manager service connection with an existing service principal ](https://docs.microsoft.com/vsts/pipelines/library/connect-to-azure?view=vsts#create-an-azure-resource-manager-service-connection-with-an-existing-service-principal) article to create a service connection with an existing service principal and use the following mapping:</span></span>

- <span data-ttu-id="c7c9b-282">Environment: AzureStack</span><span class="sxs-lookup"><span data-stu-id="c7c9b-282">Environment: AzureStack</span></span>
- <span data-ttu-id="c7c9b-283">Environment URL: Something like `https://management.local.azurestack.external`</span><span class="sxs-lookup"><span data-stu-id="c7c9b-283">Environment URL: Something like `https://management.local.azurestack.external`</span></span>
- <span data-ttu-id="c7c9b-284">Subscription ID: User subscription ID from Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c7c9b-284">Subscription ID: User subscription ID from Azure Stack</span></span>
- <span data-ttu-id="c7c9b-285">Subscription name: User subscription name from Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c7c9b-285">Subscription name: User subscription name from Azure Stack</span></span>
- <span data-ttu-id="c7c9b-286">Service Principal client ID: The principal ID from [this](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-pipeline#create-a-service-principal) section in this article.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-286">Service Principal client ID: The principal ID from [this](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-pipeline#create-a-service-principal) section in this article.</span></span>
- <span data-ttu-id="c7c9b-287">Service Principal key: The key from the same article (or the password if you used the script).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-287">Service Principal key: The key from the same article (or the password if you used the script).</span></span>
- <span data-ttu-id="c7c9b-288">Tenant ID: The tenant ID you retrieve following the instruction at [Get the tenant ID](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-pipeline#get-the-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-288">Tenant ID: The tenant ID you retrieve following the instruction at [Get the tenant ID](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-pipeline#get-the-tenant-id).</span></span>

<span data-ttu-id="c7c9b-289">Now that the endpoint is created, the VSTS to Azure Stack connection is ready to use.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-289">Now that the endpoint is created, the VSTS to Azure Stack connection is ready to use.</span></span> <span data-ttu-id="c7c9b-290">The build agent in Azure Stack gets instructions from VSTS, and then the agent conveys endpoint information for communication with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-290">The build agent in Azure Stack gets instructions from VSTS, and then the agent conveys endpoint information for communication with Azure Stack.</span></span>

![Build agent](media\azure-stack-solution-hybrid-pipeline\016_save_changes.png)

## <a name="develop-your-application-build"></a><span data-ttu-id="c7c9b-292">Develop your application build</span><span class="sxs-lookup"><span data-stu-id="c7c9b-292">Develop your application build</span></span>

<span data-ttu-id="c7c9b-293">In this part of the tutorial you'll:</span><span class="sxs-lookup"><span data-stu-id="c7c9b-293">In this part of the tutorial you'll:</span></span>

* <span data-ttu-id="c7c9b-294">Add code to an Azure DevOps Services project.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-294">Add code to an Azure DevOps Services project.</span></span>
* <span data-ttu-id="c7c9b-295">Create self-contained web app deployment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-295">Create self-contained web app deployment.</span></span>
* <span data-ttu-id="c7c9b-296">Configure the continuous deployment process</span><span class="sxs-lookup"><span data-stu-id="c7c9b-296">Configure the continuous deployment process</span></span>

> [!Note]
 > <span data-ttu-id="c7c9b-297">Your Azure Stack environment needs the correct images syndicated to run Windows Server and SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-297">Your Azure Stack environment needs the correct images syndicated to run Windows Server and SQL Server.</span></span> <span data-ttu-id="c7c9b-298">It must also have App Service deployed.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-298">It must also have App Service deployed.</span></span> <span data-ttu-id="c7c9b-299">Review the App Service documentation "Prerequisites" section for Azure Stack Operator Requirements.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-299">Review the App Service documentation "Prerequisites" section for Azure Stack Operator Requirements.</span></span>

<span data-ttu-id="c7c9b-300">Hybrid CI/CD can apply to both application code and infrastructure code.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-300">Hybrid CI/CD can apply to both application code and infrastructure code.</span></span> <span data-ttu-id="c7c9b-301">Use [Azure Resource Manager templates like web ](https://azure.microsoft.com/resources/templates/) app code from Azure DevOps Services to deploy to both clouds.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-301">Use [Azure Resource Manager templates like web ](https://azure.microsoft.com/resources/templates/) app code from Azure DevOps Services to deploy to both clouds.</span></span>

### <a name="add-code-to-an-azure-devops-services-project"></a><span data-ttu-id="c7c9b-302">Add code to an Azure DevOps Services project</span><span class="sxs-lookup"><span data-stu-id="c7c9b-302">Add code to an Azure DevOps Services project</span></span>

1. <span data-ttu-id="c7c9b-303">Sign in to Azure DevOps Services with an organization that has project creation rights on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-303">Sign in to Azure DevOps Services with an organization that has project creation rights on Azure Stack.</span></span> <span data-ttu-id="c7c9b-304">The next screen capture shows how to connect to the HybridCICD project.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-304">The next screen capture shows how to connect to the HybridCICD project.</span></span>

    ![Connect to a Project](media\azure-stack-solution-hybrid-pipeline\017_connect_to_project.png)

2. <span data-ttu-id="c7c9b-306">**Clone the repository** by creating and opening the default web app.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-306">**Clone the repository** by creating and opening the default web app.</span></span>

    ![Clone repository](media\azure-stack-solution-hybrid-pipeline\018_link_arm.png)

### <a name="create-self-contained-web-app-deployment-for-app-services-in-both-clouds"></a><span data-ttu-id="c7c9b-308">Create self-contained web app deployment for App Services in both clouds</span><span class="sxs-lookup"><span data-stu-id="c7c9b-308">Create self-contained web app deployment for App Services in both clouds</span></span>

1. <span data-ttu-id="c7c9b-309">Edit the **WebApplication.csproj** file: Select **Runtimeidentifier** and then add `win10-x64.` For more information, see [Self-contained deployment](https://docs.microsoft.com/dotnet/core/deploying/#self-contained-deployments-scd) documentation.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-309">Edit the **WebApplication.csproj** file: Select **Runtimeidentifier** and then add `win10-x64.` For more information, see [Self-contained deployment](https://docs.microsoft.com/dotnet/core/deploying/#self-contained-deployments-scd) documentation.</span></span>

    ![Configure Runtimeidentifier](media\azure-stack-solution-hybrid-pipeline\019_runtimeidentifer.png)

2. <span data-ttu-id="c7c9b-311">Use Team Explorer to check the code into Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-311">Use Team Explorer to check the code into Azure DevOps Services.</span></span>

3. <span data-ttu-id="c7c9b-312">Confirm that the application code was checked into Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-312">Confirm that the application code was checked into Azure DevOps Services.</span></span>

### <a name="create-the-build-pipeline"></a><span data-ttu-id="c7c9b-313">Create the build pipeline</span><span class="sxs-lookup"><span data-stu-id="c7c9b-313">Create the build pipeline</span></span>

1. <span data-ttu-id="c7c9b-314">Sign in to Azure DevOps Services with an organization that can create a build pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-314">Sign in to Azure DevOps Services with an organization that can create a build pipeline.</span></span>

2. <span data-ttu-id="c7c9b-315">Navigate to the **Build Web Applicaiton** page for the project.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-315">Navigate to the **Build Web Applicaiton** page for the project.</span></span>

3. <span data-ttu-id="c7c9b-316">In **Arguments**, add **-r win10-x64** code.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-316">In **Arguments**, add **-r win10-x64** code.</span></span> <span data-ttu-id="c7c9b-317">This is required to trigger a self-contained deployment with .Net Core.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-317">This is required to trigger a self-contained deployment with .Net Core.</span></span>

    ![Add argument build pipeline](media\azure-stack-solution-hybrid-pipeline\020_publish_additions.png)

4. <span data-ttu-id="c7c9b-319">Run the build.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-319">Run the build.</span></span> <span data-ttu-id="c7c9b-320">The [self-contained deployment build](https://docs.microsoft.com/dotnet/core/deploying/#self-contained-deployments-scd) process will publish artifacts that can run on Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-320">The [self-contained deployment build](https://docs.microsoft.com/dotnet/core/deploying/#self-contained-deployments-scd) process will publish artifacts that can run on Azure and Azure Stack.</span></span>

### <a name="use-an-azure-hosted-build-agent"></a><span data-ttu-id="c7c9b-321">Use an Azure hosted build agent</span><span class="sxs-lookup"><span data-stu-id="c7c9b-321">Use an Azure hosted build agent</span></span>

<span data-ttu-id="c7c9b-322">Using a hosted build agent in Azure DevOps Services is a convenient option for building and deploying web apps.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-322">Using a hosted build agent in Azure DevOps Services is a convenient option for building and deploying web apps.</span></span> <span data-ttu-id="c7c9b-323">Agent maintenance and upgrades are automatically performed by Microsoft Azure, which enables a continuous and uninterrupted development cycle.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-323">Agent maintenance and upgrades are automatically performed by Microsoft Azure, which enables a continuous and uninterrupted development cycle.</span></span>

### <a name="configure-the-continuous-deployment-cd-process"></a><span data-ttu-id="c7c9b-324">Configure the continuous deployment (CD) process</span><span class="sxs-lookup"><span data-stu-id="c7c9b-324">Configure the continuous deployment (CD) process</span></span>

<span data-ttu-id="c7c9b-325">Azure DevOps Services and Team Foundation Server (TFS) provide a highly configurable and manageable pipeline for releases to multiple environments such as development, staging, quality assurance (QA), and production.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-325">Azure DevOps Services and Team Foundation Server (TFS) provide a highly configurable and manageable pipeline for releases to multiple environments such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="c7c9b-326">This process can include requiring approvals at specific stages of the application life cycle.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-326">This process can include requiring approvals at specific stages of the application life cycle.</span></span>

### <a name="create-release-pipeline"></a><span data-ttu-id="c7c9b-327">Create release pipeline</span><span class="sxs-lookup"><span data-stu-id="c7c9b-327">Create release pipeline</span></span>

<span data-ttu-id="c7c9b-328">Creating a release pipeline is the final step in your application build process.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-328">Creating a release pipeline is the final step in your application build process.</span></span> <span data-ttu-id="c7c9b-329">This release pipeline is used to create a release and deploy a build.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-329">This release pipeline is used to create a release and deploy a build.</span></span>

1. <span data-ttu-id="c7c9b-330">Sign in to Azure DevOps Services and navigate to **Azure Pipelines** for your project.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-330">Sign in to Azure DevOps Services and navigate to **Azure Pipelines** for your project.</span></span>
2. <span data-ttu-id="c7c9b-331">On the **Releases** tab, select **\[ + ]**  and then pick **Create release definition**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-331">On the **Releases** tab, select **\[ + ]**  and then pick **Create release definition**.</span></span>

   ![Create release pipeline](media\azure-stack-solution-hybrid-pipeline\021a_releasedef.png)

3. <span data-ttu-id="c7c9b-333">On **Select a Template**, choose **Azure App Service Deployment**, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-333">On **Select a Template**, choose **Azure App Service Deployment**, and then select **Apply**.</span></span>

    ![Apply template](media\azure-stack-solution-hybrid-pipeline\102.png)

4. <span data-ttu-id="c7c9b-335">On **Add artifact**, from the **Source (Build definition)** pull-down menu, select the Azure Cloud build app.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-335">On **Add artifact**, from the **Source (Build definition)** pull-down menu, select the Azure Cloud build app.</span></span>

    ![Add artifact](media\azure-stack-solution-hybrid-pipeline\103.png)

5. <span data-ttu-id="c7c9b-337">On the **Pipeline** tab, select the **1 Phase**, **1 Task** link to **View environment tasks**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-337">On the **Pipeline** tab, select the **1 Phase**, **1 Task** link to **View environment tasks**.</span></span>

    ![Pipeline view tasks](media\azure-stack-solution-hybrid-pipeline\104.png)

6. <span data-ttu-id="c7c9b-339">On the **Tasks** tab, enter Azure as the **Environment name** and select the AzureCloud Traders-Web EP from the **Azure subscription** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-339">On the **Tasks** tab, enter Azure as the **Environment name** and select the AzureCloud Traders-Web EP from the **Azure subscription** drop-down list.</span></span>

    ![Set environment variables](media\azure-stack-solution-hybrid-pipeline\105.png)

7. <span data-ttu-id="c7c9b-341">Enter the **Azure app service name**, which is "northwindtraders" in the next screen capture.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-341">Enter the **Azure app service name**, which is "northwindtraders" in the next screen capture.</span></span>

    ![App service name](media\azure-stack-solution-hybrid-pipeline\106.png)

8. <span data-ttu-id="c7c9b-343">For the Agent phase, select **Hosted VS2017** from the **Agent queue** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-343">For the Agent phase, select **Hosted VS2017** from the **Agent queue** drop-down list.</span></span>

    ![Hosted agent](media\azure-stack-solution-hybrid-pipeline\107.png)

9. <span data-ttu-id="c7c9b-345">In **Deploy Azure App Service**, select the valid **Package or folder** for the environment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-345">In **Deploy Azure App Service**, select the valid **Package or folder** for the environment.</span></span>

    ![Select package or folder](media\azure-stack-solution-hybrid-pipeline\108.png)

10. <span data-ttu-id="c7c9b-347">In **Select File or Folder**, select **OK** to **Location**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-347">In **Select File or Folder**, select **OK** to **Location**.</span></span>

    ![Alt Text](media\azure-stack-solution-hybrid-pipeline\109.png)

11. <span data-ttu-id="c7c9b-349">Save all changes and go back to **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-349">Save all changes and go back to **Pipeline**.</span></span>

    ![Alt Text](media\azure-stack-solution-hybrid-pipeline\110.png)

12. <span data-ttu-id="c7c9b-351">On the **Pipeline** tab, select **Add artifact**, and choose the **NorthwindCloud Traders-Vessel** from the **Source (Build Definition)** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-351">On the **Pipeline** tab, select **Add artifact**, and choose the **NorthwindCloud Traders-Vessel** from the **Source (Build Definition)** drop-down list.</span></span>

    ![Add new artifact](media\azure-stack-solution-hybrid-pipeline\111.png)

13. <span data-ttu-id="c7c9b-353">On **Select a Template**, add another environment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-353">On **Select a Template**, add another environment.</span></span> <span data-ttu-id="c7c9b-354">Pick **Azure App Service Deployment** and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-354">Pick **Azure App Service Deployment** and then select **Apply**.</span></span>

    ![Select template](media\azure-stack-solution-hybrid-pipeline\112.png)

14. <span data-ttu-id="c7c9b-356">Enter "Azure Stack" as the **Environment name**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-356">Enter "Azure Stack" as the **Environment name**.</span></span>

    ![Environment name](media\azure-stack-solution-hybrid-pipeline\113.png)

15. <span data-ttu-id="c7c9b-358">On the **Tasks** tab, find and select Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-358">On the **Tasks** tab, find and select Azure Stack.</span></span>

    ![Azure Stack environment](media\azure-stack-solution-hybrid-pipeline\114.png)

16. <span data-ttu-id="c7c9b-360">From the **Azure subscription** drop-down list, select  "AzureStack Traders-Vessel EP" for the Azure Stack endpoint.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-360">From the **Azure subscription** drop-down list, select  "AzureStack Traders-Vessel EP" for the Azure Stack endpoint.</span></span>

    ![Alt Text](media\azure-stack-solution-hybrid-pipeline\115.png)

17. <span data-ttu-id="c7c9b-362">Enter the Azure Stack web app name as the **App service name**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-362">Enter the Azure Stack web app name as the **App service name**.</span></span>

    ![App service name](media\azure-stack-solution-hybrid-pipeline\116.png)

18. <span data-ttu-id="c7c9b-364">Under **Agent selection**, pick "AzureStack -bDouglas Fir" from the **Agent queue** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-364">Under **Agent selection**, pick "AzureStack -bDouglas Fir" from the **Agent queue** drop-down list.</span></span>

    ![Pick agent](media\azure-stack-solution-hybrid-pipeline\117.png)

19. <span data-ttu-id="c7c9b-366">For **Deploy Azure App Service**, select the valid **Package or folder** for the environment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-366">For **Deploy Azure App Service**, select the valid **Package or folder** for the environment.</span></span> <span data-ttu-id="c7c9b-367">On **Select File Or Folder**, select **OK** for the folder **Location**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-367">On **Select File Or Folder**, select **OK** for the folder **Location**.</span></span>

    ![Pick package or folder](media\azure-stack-solution-hybrid-pipeline\118.png)

    ![Approve location](media\azure-stack-solution-hybrid-pipeline\119.png)

20. <span data-ttu-id="c7c9b-370">On the **Variable** tab, find the variable named **VSTS_ARM_REST_IGNORE_SSL_ERRORS**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-370">On the **Variable** tab, find the variable named **VSTS_ARM_REST_IGNORE_SSL_ERRORS**.</span></span> <span data-ttu-id="c7c9b-371">Set the variable value to **true**, and set its scope to **Azure Stack**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-371">Set the variable value to **true**, and set its scope to **Azure Stack**.</span></span>

    ![Configure variable](media\azure-stack-solution-hybrid-pipeline\120.png)

21. <span data-ttu-id="c7c9b-373">On the **Pipeline** tab, select the **Continuous deployment trigger** icon for the NorthwindCloud Traders-Web artifact and set the **Continuous deployment trigger** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-373">On the **Pipeline** tab, select the **Continuous deployment trigger** icon for the NorthwindCloud Traders-Web artifact and set the **Continuous deployment trigger** to **Enabled**.</span></span>  <span data-ttu-id="c7c9b-374">Do the same thing for the "NorthwindCloud Traders-Vessel" artifact.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-374">Do the same thing for the "NorthwindCloud Traders-Vessel" artifact.</span></span>

    ![Set continuous deployment trigger](media\azure-stack-solution-hybrid-pipeline\121.png)

22. <span data-ttu-id="c7c9b-376">For the Azure Stack environment, select the **Pre-deployment conditions** icon set the trigger to **After release**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-376">For the Azure Stack environment, select the **Pre-deployment conditions** icon set the trigger to **After release**.</span></span>

    ![Set pre-deployment conditions trigger](media\azure-stack-solution-hybrid-pipeline\122.png)

23. <span data-ttu-id="c7c9b-378">Save all your changes.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-378">Save all your changes.</span></span>

> [!Note]
> <span data-ttu-id="c7c9b-379">Some settings for release tasks may have been automatically defined as [environment variables](https://docs.microsoft.com/azure/devops/pipelines/release/variables?view=vsts#custom-variables) when you created a release pipeline from a template.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-379">Some settings for release tasks may have been automatically defined as [environment variables](https://docs.microsoft.com/azure/devops/pipelines/release/variables?view=vsts#custom-variables) when you created a release pipeline from a template.</span></span> <span data-ttu-id="c7c9b-380">These settings can't be modified in the task settings.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-380">These settings can't be modified in the task settings.</span></span> <span data-ttu-id="c7c9b-381">However, you can edit these settings in the parent environment items.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-381">However, you can edit these settings in the parent environment items.</span></span>

## <a name="create-a-release"></a><span data-ttu-id="c7c9b-382">Create a release</span><span class="sxs-lookup"><span data-stu-id="c7c9b-382">Create a release</span></span>

<span data-ttu-id="c7c9b-383">Now that you have completed the modifications to the release pipeline, it's time to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-383">Now that you have completed the modifications to the release pipeline, it's time to start the deployment.</span></span> <span data-ttu-id="c7c9b-384">To do this, you create a release from the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-384">To do this, you create a release from the release pipeline.</span></span> <span data-ttu-id="c7c9b-385">A release may be created automatically; for example, the continuous deployment trigger is set in the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-385">A release may be created automatically; for example, the continuous deployment trigger is set in the release pipeline.</span></span> <span data-ttu-id="c7c9b-386">This means that modifying the source code will start a new build and, from that, a new release.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-386">This means that modifying the source code will start a new build and, from that, a new release.</span></span> <span data-ttu-id="c7c9b-387">However, in this section you will create a new release manually.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-387">However, in this section you will create a new release manually.</span></span>

1. <span data-ttu-id="c7c9b-388">On the **Pipeline** tab, open the **Release** drop-down list and choose **Create release**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-388">On the **Pipeline** tab, open the **Release** drop-down list and choose **Create release**.</span></span>

    ![Create a release](media\azure-stack-solution-hybrid-pipeline\200.png)

2. <span data-ttu-id="c7c9b-390">Enter a description for the release, check to see that the correct artifacts are selected, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-390">Enter a description for the release, check to see that the correct artifacts are selected, and then choose **Create**.</span></span> <span data-ttu-id="c7c9b-391">After a few moments, a banner appears indicating that the new release was created, and the release name is displayed as a link.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-391">After a few moments, a banner appears indicating that the new release was created, and the release name is displayed as a link.</span></span> <span data-ttu-id="c7c9b-392">Choose the link to see the release summary page.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-392">Choose the link to see the release summary page.</span></span>

    ![Release creation banner](media\azure-stack-solution-hybrid-pipeline\201.png)

3. <span data-ttu-id="c7c9b-394">The release summary page for shows details about the release.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-394">The release summary page for shows details about the release.</span></span> <span data-ttu-id="c7c9b-395">In the following screen capture for "Release-2", the **Environments** section shows the **Deployment status** for the Azure as "IN PROGRESS", and the status for Azure Stack is "SUCCEEDED".</span><span class="sxs-lookup"><span data-stu-id="c7c9b-395">In the following screen capture for "Release-2", the **Environments** section shows the **Deployment status** for the Azure as "IN PROGRESS", and the status for Azure Stack is "SUCCEEDED".</span></span> <span data-ttu-id="c7c9b-396">When the deployment status for the Azure environment changes to "SUCCEEDED", a banner appears indicating that the release is ready for approval.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-396">When the deployment status for the Azure environment changes to "SUCCEEDED", a banner appears indicating that the release is ready for approval.</span></span> <span data-ttu-id="c7c9b-397">When a deployment is pending or has failed, a blue **(i)** information icon is shown.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-397">When a deployment is pending or has failed, a blue **(i)** information icon is shown.</span></span> <span data-ttu-id="c7c9b-398">Hover over the icon to see a pop-up that contains the reason for delay or failure.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-398">Hover over the icon to see a pop-up that contains the reason for delay or failure.</span></span>

    ![Release summary page](media\azure-stack-solution-hybrid-pipeline\202.png)

<span data-ttu-id="c7c9b-400">Other views, such as the list of releases, will also display an icon that indicates approval is pending.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-400">Other views, such as the list of releases, will also display an icon that indicates approval is pending.</span></span> <span data-ttu-id="c7c9b-401">The pop-up for this icon shows the environment name and more details related to the deployment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-401">The pop-up for this icon shows the environment name and more details related to the deployment.</span></span> <span data-ttu-id="c7c9b-402">It's easy for an administrator see the overall progress of releases and see which releases are waiting for approval.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-402">It's easy for an administrator see the overall progress of releases and see which releases are waiting for approval.</span></span>

### <a name="monitor-and-track-deployments"></a><span data-ttu-id="c7c9b-403">Monitor and track deployments</span><span class="sxs-lookup"><span data-stu-id="c7c9b-403">Monitor and track deployments</span></span>

<span data-ttu-id="c7c9b-404">This section shows how you can monitor and track all your deployments.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-404">This section shows how you can monitor and track all your deployments.</span></span> <span data-ttu-id="c7c9b-405">The release for deploying the two Azure App Services websites provides a good example.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-405">The release for deploying the two Azure App Services websites provides a good example.</span></span>

1. <span data-ttu-id="c7c9b-406">On the "Release-2" summary page, select **Logs**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-406">On the "Release-2" summary page, select **Logs**.</span></span> <span data-ttu-id="c7c9b-407">During a deployment, this page shows the live log from the agent.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-407">During a deployment, this page shows the live log from the agent.</span></span> <span data-ttu-id="c7c9b-408">The left pane shows the status of each operation in the deployment for each environment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-408">The left pane shows the status of each operation in the deployment for each environment.</span></span>

    <span data-ttu-id="c7c9b-409">You can choose a person icon in the **Action** column for a Pre-deployment or Post-deployment approval to see who approved (or rejected) the deployment, and the message they provided.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-409">You can choose a person icon in the **Action** column for a Pre-deployment or Post-deployment approval to see who approved (or rejected) the deployment, and the message they provided.</span></span>

2. <span data-ttu-id="c7c9b-410">After the deployment finishes, the entire log file is displayed in the right pane.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-410">After the deployment finishes, the entire log file is displayed in the right pane.</span></span> <span data-ttu-id="c7c9b-411">You can select any **Step** in the left pane to see the log file for a single step, such as "Initialize Job".</span><span class="sxs-lookup"><span data-stu-id="c7c9b-411">You can select any **Step** in the left pane to see the log file for a single step, such as "Initialize Job".</span></span> <span data-ttu-id="c7c9b-412">The ability to see individual logs makes it easier to trace and debug  parts of the overall deployment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-412">The ability to see individual logs makes it easier to trace and debug  parts of the overall deployment.</span></span> <span data-ttu-id="c7c9b-413">You can also **Save** the log file for a step, or **Download all logs as zip**.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-413">You can also **Save** the log file for a step, or **Download all logs as zip**.</span></span>

    ![Release logs](media\azure-stack-solution-hybrid-pipeline\203.png)

3. <span data-ttu-id="c7c9b-415">Open the **Summary** tab to see general information about the release.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-415">Open the **Summary** tab to see general information about the release.</span></span> <span data-ttu-id="c7c9b-416">This view shows details about the build, the environments it was deployed to, deployment status, and other information about the release.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-416">This view shows details about the build, the environments it was deployed to, deployment status, and other information about the release.</span></span>

4. <span data-ttu-id="c7c9b-417">Select an environment link (**Azure** or **Azure Stack**) to see information about existing and pending deployments to a specific environment.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-417">Select an environment link (**Azure** or **Azure Stack**) to see information about existing and pending deployments to a specific environment.</span></span> <span data-ttu-id="c7c9b-418">You can use these views as a quick way to verify that the same build was deployed to both environments.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-418">You can use these views as a quick way to verify that the same build was deployed to both environments.</span></span>

5. <span data-ttu-id="c7c9b-419">Open the **deployed production app** in your browser.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-419">Open the **deployed production app** in your browser.</span></span> <span data-ttu-id="c7c9b-420">For example, for the Azure App Services website, open the URL `http://[your-app-name].azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c7c9b-420">For example, for the Azure App Services website, open the URL `http://[your-app-name].azurewebsites.net`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7c9b-421">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7c9b-421">Next steps</span></span>

* <span data-ttu-id="c7c9b-422">To learn more about Azure Cloud Patterns, see [Cloud Design Patterns](https://docs.microsoft.com/azure/architecture/patterns).</span><span class="sxs-lookup"><span data-stu-id="c7c9b-422">To learn more about Azure Cloud Patterns, see [Cloud Design Patterns](https://docs.microsoft.com/azure/architecture/patterns).</span></span>
