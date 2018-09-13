---
title: In this tutorial, you create an Azure Stack VM using a template | Microsoft Docs
description: Describes how to use the ASDK to create a VM using a predfined template and a GitHub custom template.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: 5026a7a753ec744d281266b2fb30a70a66a7f9db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965441"
---
# <a name="tutorial-create-a-vm-using-a-community-template"></a><span data-ttu-id="18158-103">Tutorial: create a VM using a community template</span><span class="sxs-lookup"><span data-stu-id="18158-103">Tutorial: create a VM using a community template</span></span>
<span data-ttu-id="18158-104">As an Azure Stack operator or user, you can create a VM using [custom GitHub quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) rather than deploying one manually from the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="18158-104">As an Azure Stack operator or user, you can create a VM using [custom GitHub quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) rather than deploying one manually from the Azure Stack marketplace.</span></span>

<span data-ttu-id="18158-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="18158-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18158-106">Learn about Azure Stack quickstart templates</span><span class="sxs-lookup"><span data-stu-id="18158-106">Learn about Azure Stack quickstart templates</span></span> 
> * <span data-ttu-id="18158-107">Create a VM using a custom GitHub template</span><span class="sxs-lookup"><span data-stu-id="18158-107">Create a VM using a custom GitHub template</span></span>
> * <span data-ttu-id="18158-108">Start minikube and install an application</span><span class="sxs-lookup"><span data-stu-id="18158-108">Start minikube and install an application</span></span>

## <a name="learn-about-azure-stack-quickstart-templates"></a><span data-ttu-id="18158-109">Learn about Azure Stack quickstart templates</span><span class="sxs-lookup"><span data-stu-id="18158-109">Learn about Azure Stack quickstart templates</span></span>
<span data-ttu-id="18158-110">Azure Stack quickstart templates are stored in the [public AzureStack QuickStart Templates repository](https://github.com/Azure/AzureStack-QuickStart-Templates) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="18158-110">Azure Stack quickstart templates are stored in the [public AzureStack QuickStart Templates repository](https://github.com/Azure/AzureStack-QuickStart-Templates) on GitHub.</span></span> <span data-ttu-id="18158-111">This repository contains Azure Resource Manager deployment templates that have been tested with the Microsoft Azure Stack Development Kit (ASDK).</span><span class="sxs-lookup"><span data-stu-id="18158-111">This repository contains Azure Resource Manager deployment templates that have been tested with the Microsoft Azure Stack Development Kit (ASDK).</span></span> <span data-ttu-id="18158-112">You can use them to make it easier for you to evaluate Azure Stack and use the ASDK environment.</span><span class="sxs-lookup"><span data-stu-id="18158-112">You can use them to make it easier for you to evaluate Azure Stack and use the ASDK environment.</span></span> 

<span data-ttu-id="18158-113">Over time many GitHub users have contributed to the repository, resulting in a huge collection of more than 400 deployment templates.</span><span class="sxs-lookup"><span data-stu-id="18158-113">Over time many GitHub users have contributed to the repository, resulting in a huge collection of more than 400 deployment templates.</span></span> <span data-ttu-id="18158-114">This repository is a great starting point to get a better understanding of how you can deploy various kinds of environments to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="18158-114">This repository is a great starting point to get a better understanding of how you can deploy various kinds of environments to Azure Stack.</span></span> 

>[!IMPORTANT]
> <span data-ttu-id="18158-115">Some of these templates are created by members of the community and not by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="18158-115">Some of these templates are created by members of the community and not by Microsoft.</span></span> <span data-ttu-id="18158-116">Each template is licensed under a license agreement by its owner, not Microsoft.</span><span class="sxs-lookup"><span data-stu-id="18158-116">Each template is licensed under a license agreement by its owner, not Microsoft.</span></span> <span data-ttu-id="18158-117">Microsoft is not responsible for these templates and does not screen for security, compatibility, or performance.</span><span class="sxs-lookup"><span data-stu-id="18158-117">Microsoft is not responsible for these templates and does not screen for security, compatibility, or performance.</span></span> <span data-ttu-id="18158-118">Community templates are not supported under any Microsoft support program or service, and are made available "AS IS" without warranty of any kind.</span><span class="sxs-lookup"><span data-stu-id="18158-118">Community templates are not supported under any Microsoft support program or service, and are made available "AS IS" without warranty of any kind.</span></span>

<span data-ttu-id="18158-119">If you want to contribute your Azure Resource Manager templates to GitHub, you should make your contribution to the [azure-quickstart-templates repository](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="18158-119">If you want to contribute your Azure Resource Manager templates to GitHub, you should make your contribution to the [azure-quickstart-templates repository](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

<span data-ttu-id="18158-120">To learn more about the GitHub repository, and how to contribute to it, see the [repo's readme file](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="18158-120">To learn more about the GitHub repository, and how to contribute to it, see the [repo's readme file](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md).</span></span> 


## <a name="create-a-vm-using-a-custom-github-template"></a><span data-ttu-id="18158-121">Create a VM using a custom GitHub template</span><span class="sxs-lookup"><span data-stu-id="18158-121">Create a VM using a custom GitHub template</span></span>
<span data-ttu-id="18158-122">In this example tutorial, the [101-vm-linux-minikube](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-linux-minikube) Azure Stack quickstart template is used to deploy an Ubuntu 16.04 virtual machine on AzureStack running Minikube to manage a kubenetes cluster.</span><span class="sxs-lookup"><span data-stu-id="18158-122">In this example tutorial, the [101-vm-linux-minikube](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-linux-minikube) Azure Stack quickstart template is used to deploy an Ubuntu 16.04 virtual machine on AzureStack running Minikube to manage a kubenetes cluster.</span></span>

<span data-ttu-id="18158-123">Minikube is a tool that makes it easy to run Kubernetes locally.</span><span class="sxs-lookup"><span data-stu-id="18158-123">Minikube is a tool that makes it easy to run Kubernetes locally.</span></span> <span data-ttu-id="18158-124">Minikube runs a single-node Kubernetes cluster inside a VM for users looking to try out Kubernetes or develop with it day-to-day.</span><span class="sxs-lookup"><span data-stu-id="18158-124">Minikube runs a single-node Kubernetes cluster inside a VM for users looking to try out Kubernetes or develop with it day-to-day.</span></span> <span data-ttu-id="18158-125">It supports a simple, one node Kubernetes cluster running on a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="18158-125">It supports a simple, one node Kubernetes cluster running on a Linux VM.</span></span> <span data-ttu-id="18158-126">It’s the fastest and most straight forward way to get a fully functional Kubernetes cluster running.</span><span class="sxs-lookup"><span data-stu-id="18158-126">It’s the fastest and most straight forward way to get a fully functional Kubernetes cluster running.</span></span> <span data-ttu-id="18158-127">It allows developers to develop and test their Kubernetes-based application deployments on their local machines.</span><span class="sxs-lookup"><span data-stu-id="18158-127">It allows developers to develop and test their Kubernetes-based application deployments on their local machines.</span></span> <span data-ttu-id="18158-128">Architecturally, Minikube VM runs both Master and Agent Node Components locally:</span><span class="sxs-lookup"><span data-stu-id="18158-128">Architecturally, Minikube VM runs both Master and Agent Node Components locally:</span></span>
- <span data-ttu-id="18158-129">Master Node components such as API Server, Scheduler, and etcd Server are run in a single Linux process called LocalKube.</span><span class="sxs-lookup"><span data-stu-id="18158-129">Master Node components such as API Server, Scheduler, and etcd Server are run in a single Linux process called LocalKube.</span></span>
- <span data-ttu-id="18158-130">Agent Node components are run inside docker containers exactly as they would run on a normal Agent Node.</span><span class="sxs-lookup"><span data-stu-id="18158-130">Agent Node components are run inside docker containers exactly as they would run on a normal Agent Node.</span></span> <span data-ttu-id="18158-131">From an application deployment standpoint, there is no difference when the application is deployed on a Minikube or regular Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="18158-131">From an application deployment standpoint, there is no difference when the application is deployed on a Minikube or regular Kubernetes cluster.</span></span>

<span data-ttu-id="18158-132">This template installs the following components:</span><span class="sxs-lookup"><span data-stu-id="18158-132">This template installs the following components:</span></span>

- <span data-ttu-id="18158-133">Ubuntu 16.04 LTS VM</span><span class="sxs-lookup"><span data-stu-id="18158-133">Ubuntu 16.04 LTS VM</span></span>
- [<span data-ttu-id="18158-134">Docker-CE</span><span class="sxs-lookup"><span data-stu-id="18158-134">Docker-CE</span></span>](https://download.docker.com/linux/ubuntu) 
- [<span data-ttu-id="18158-135">Kubectl</span><span class="sxs-lookup"><span data-stu-id="18158-135">Kubectl</span></span>](https://storage.googleapis.com/kubernetes-release/release/v1.8.0/bin/linux/amd64/kubectl)
- [<span data-ttu-id="18158-136">Minikube</span><span class="sxs-lookup"><span data-stu-id="18158-136">Minikube</span></span>](https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64)
- <span data-ttu-id="18158-137">xFCE4</span><span class="sxs-lookup"><span data-stu-id="18158-137">xFCE4</span></span>
- <span data-ttu-id="18158-138">xRDP</span><span class="sxs-lookup"><span data-stu-id="18158-138">xRDP</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18158-139">The Ubuntu VM image (Ubuntu Server 16.04 LTS in this example) must already have been added to the Azure Stack marketplace before beginning these steps.</span><span class="sxs-lookup"><span data-stu-id="18158-139">The Ubuntu VM image (Ubuntu Server 16.04 LTS in this example) must already have been added to the Azure Stack marketplace before beginning these steps.</span></span>

1.  <span data-ttu-id="18158-140">Click **+New** > **Custom** > **Template deployment**.</span><span class="sxs-lookup"><span data-stu-id="18158-140">Click **+New** > **Custom** > **Template deployment**.</span></span>

    ![](media/azure-stack-create-vm-template/1.PNG) 

2. <span data-ttu-id="18158-141">Click **Edit template**.</span><span class="sxs-lookup"><span data-stu-id="18158-141">Click **Edit template**.</span></span>

   ![](media/azure-stack-create-vm-template/2.PNG) 

3.  <span data-ttu-id="18158-142">Click **Quickstart template**.</span><span class="sxs-lookup"><span data-stu-id="18158-142">Click **Quickstart template**.</span></span>

       ![](media/azure-stack-create-vm-template/3.PNG)

4. <span data-ttu-id="18158-143">Select **101-vm-linux-minikube** from the available templates using the **Select a template** dropdown list, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="18158-143">Select **101-vm-linux-minikube** from the available templates using the **Select a template** dropdown list, and then click **OK**.</span></span>  

   ![](media/azure-stack-create-vm-template/4.PNG)

5. <span data-ttu-id="18158-144">If you want to make modifications to the template JSON you can do so, if not, or when complete, click **Save** to close the edit template dialog.</span><span class="sxs-lookup"><span data-stu-id="18158-144">If you want to make modifications to the template JSON you can do so, if not, or when complete, click **Save** to close the edit template dialog.</span></span>

   ![](media/azure-stack-create-vm-template/5.PNG) 

6.  <span data-ttu-id="18158-145">Click on **Parameters**, fill in or modify the available fields as necessary, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="18158-145">Click on **Parameters**, fill in or modify the available fields as necessary, and then click **OK**.</span></span> <span data-ttu-id="18158-146">Choose the subscription to use, create or choose an existing resource group name, and then click **Create** to initiate the template deployment.</span><span class="sxs-lookup"><span data-stu-id="18158-146">Choose the subscription to use, create or choose an existing resource group name, and then click **Create** to initiate the template deployment.</span></span>

       ![](media/azure-stack-create-vm-template/6.PNG)

7. <span data-ttu-id="18158-147">Choose the subscription to use, create or choose an existing resource group name, and then click **Create** to initiate the template deployment.</span><span class="sxs-lookup"><span data-stu-id="18158-147">Choose the subscription to use, create or choose an existing resource group name, and then click **Create** to initiate the template deployment.</span></span>

   ![](media/azure-stack-create-vm-template/7.PNG)

8. <span data-ttu-id="18158-148">The resource group deployment takes several minutes to create the custom template-based VM.</span><span class="sxs-lookup"><span data-stu-id="18158-148">The resource group deployment takes several minutes to create the custom template-based VM.</span></span> <span data-ttu-id="18158-149">You can monitor the installation status through notifications and from the resource group properties.</span><span class="sxs-lookup"><span data-stu-id="18158-149">You can monitor the installation status through notifications and from the resource group properties.</span></span> 

   ![](media/azure-stack-create-vm-template/8.PNG)

   >[!NOTE]
   > <span data-ttu-id="18158-150">The VM will be running when the deployment completes.</span><span class="sxs-lookup"><span data-stu-id="18158-150">The VM will be running when the deployment completes.</span></span> 

## <a name="start-minikube-and-install-an-application"></a><span data-ttu-id="18158-151">Start minikube and install an application</span><span class="sxs-lookup"><span data-stu-id="18158-151">Start minikube and install an application</span></span>
<span data-ttu-id="18158-152">Now that the Linux VM has been successfully created, you can sign in to start minikube and install an application.</span><span class="sxs-lookup"><span data-stu-id="18158-152">Now that the Linux VM has been successfully created, you can sign in to start minikube and install an application.</span></span> 

1. <span data-ttu-id="18158-153">After the deployment completes, click **Connect** to view the Public IP address that will be used to connect to the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="18158-153">After the deployment completes, click **Connect** to view the Public IP address that will be used to connect to the Linux VM.</span></span> 

   ![](media/azure-stack-create-vm-template/9.PNG)

2. <span data-ttu-id="18158-154">From an elevated command prompt, run **mstsc.exe** to open Remote Desktop Connection and connect to the Linux VM's public IP address discovered in the previous step.</span><span class="sxs-lookup"><span data-stu-id="18158-154">From an elevated command prompt, run **mstsc.exe** to open Remote Desktop Connection and connect to the Linux VM's public IP address discovered in the previous step.</span></span> <span data-ttu-id="18158-155">When prompted to sign in to xRDP, use the credentials you specified when creating the VM.</span><span class="sxs-lookup"><span data-stu-id="18158-155">When prompted to sign in to xRDP, use the credentials you specified when creating the VM.</span></span>

   ![](media/azure-stack-create-vm-template/10.PNG)

3. <span data-ttu-id="18158-156">Open Terminal Emulator and enter following commands to start minikube:</span><span class="sxs-lookup"><span data-stu-id="18158-156">Open Terminal Emulator and enter following commands to start minikube:</span></span>

    >    `sudo minikube start --vm-driver=none`
    >   
    >    `sudo minikube addons enable dashboard`
    >    
    >    `sudo minikube dashboard --url`

   ![](media/azure-stack-create-vm-template/11.PNG)

4. <span data-ttu-id="18158-157">Open the web browser and visit the kubernetes dashboard address.</span><span class="sxs-lookup"><span data-stu-id="18158-157">Open the web browser and visit the kubernetes dashboard address.</span></span> <span data-ttu-id="18158-158">Congratulations, you now have a fully working kubernetes installation using minikube!</span><span class="sxs-lookup"><span data-stu-id="18158-158">Congratulations, you now have a fully working kubernetes installation using minikube!</span></span>

   ![](media/azure-stack-create-vm-template/12.PNG)

5. <span data-ttu-id="18158-159">If you would like to deploy a sample application, visit the official documentation page of kubernetes, skip the "Create Minikube Cluster" section as you have already created one above.</span><span class="sxs-lookup"><span data-stu-id="18158-159">If you would like to deploy a sample application, visit the official documentation page of kubernetes, skip the "Create Minikube Cluster" section as you have already created one above.</span></span> <span data-ttu-id="18158-160">Simply jump to the section "Create your Node.js application" at https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/.</span><span class="sxs-lookup"><span data-stu-id="18158-160">Simply jump to the section "Create your Node.js application" at https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18158-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="18158-161">Next steps</span></span>

<span data-ttu-id="18158-162">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="18158-162">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18158-163">Learn about Azure Stack quickstart templates</span><span class="sxs-lookup"><span data-stu-id="18158-163">Learn about Azure Stack quickstart templates</span></span> 
> * <span data-ttu-id="18158-164">Create a VM using a custom GitHub template</span><span class="sxs-lookup"><span data-stu-id="18158-164">Create a VM using a custom GitHub template</span></span>
> * <span data-ttu-id="18158-165">Start minikube and install an application</span><span class="sxs-lookup"><span data-stu-id="18158-165">Start minikube and install an application</span></span>

