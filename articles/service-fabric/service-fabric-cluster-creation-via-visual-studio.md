---
title: Setting up a Service Fabric cluster using Visual Studio | Microsoft Docs
description: Describes how to set up a Service Fabric cluster by using Azure Resource Manager template created by an Azure Resource Group project in Visual Studio
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: ''
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn@microsoft.com
ms.openlocfilehash: 7a20f222f14fb91e8ff94539aa230477afaa909e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552948"
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="1a79a-103">Set up a Service Fabric cluster by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a79a-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="1a79a-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="1a79a-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="1a79a-105">We will use a Visual Studio Azure resource group project to create the template.</span><span class="sxs-lookup"><span data-stu-id="1a79a-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="1a79a-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a79a-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="1a79a-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span><span class="sxs-lookup"><span data-stu-id="1a79a-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="1a79a-108">Create a Service Fabric cluster template by using an Azure resource group project</span><span class="sxs-lookup"><span data-stu-id="1a79a-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="1a79a-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span><span class="sxs-lookup"><span data-stu-id="1a79a-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![New Project dialog with Azure Resource Group project selected][1]

<span data-ttu-id="1a79a-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span><span class="sxs-lookup"><span data-stu-id="1a79a-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="1a79a-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span><span class="sxs-lookup"><span data-stu-id="1a79a-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="1a79a-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a79a-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="1a79a-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span><span class="sxs-lookup"><span data-stu-id="1a79a-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Select Azure Template dialog with Service Fabric Cluster template selected][2]

<span data-ttu-id="1a79a-116">Select the Service Fabric Cluster template and hit the OK button again.</span><span class="sxs-lookup"><span data-stu-id="1a79a-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="1a79a-117">The project and the Resource Manager template have now been created.</span><span class="sxs-lookup"><span data-stu-id="1a79a-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="1a79a-118">Prepare the template for deployment</span><span class="sxs-lookup"><span data-stu-id="1a79a-118">Prepare the template for deployment</span></span>
<span data-ttu-id="1a79a-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span><span class="sxs-lookup"><span data-stu-id="1a79a-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="1a79a-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span><span class="sxs-lookup"><span data-stu-id="1a79a-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="1a79a-121">Open the file and provide the following values:</span><span class="sxs-lookup"><span data-stu-id="1a79a-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="1a79a-122">Parameter name</span><span class="sxs-lookup"><span data-stu-id="1a79a-122">Parameter name</span></span> | <span data-ttu-id="1a79a-123">Description</span><span class="sxs-lookup"><span data-stu-id="1a79a-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a79a-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="1a79a-124">adminUserName</span></span> |<span data-ttu-id="1a79a-125">The name of the administrator account for Service Fabric machines (nodes).</span><span class="sxs-lookup"><span data-stu-id="1a79a-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="1a79a-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="1a79a-126">certificateThumbprint</span></span> |<span data-ttu-id="1a79a-127">The thumbprint of the certificate that secures the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="1a79a-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="1a79a-128">sourceVaultResourceId</span></span> |<span data-ttu-id="1a79a-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span><span class="sxs-lookup"><span data-stu-id="1a79a-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="1a79a-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="1a79a-130">certificateUrlValue</span></span> |<span data-ttu-id="1a79a-131">The URL of the cluster security certificate.</span><span class="sxs-lookup"><span data-stu-id="1a79a-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="1a79a-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span><span class="sxs-lookup"><span data-stu-id="1a79a-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="1a79a-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="1a79a-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="1a79a-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span><span class="sxs-lookup"><span data-stu-id="1a79a-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="1a79a-135">Optional: change the cluster name</span><span class="sxs-lookup"><span data-stu-id="1a79a-135">Optional: change the cluster name</span></span>
<span data-ttu-id="1a79a-136">Every Service Fabric cluster has a name.</span><span class="sxs-lookup"><span data-stu-id="1a79a-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="1a79a-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="1a79a-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1a79a-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="1a79a-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span><span class="sxs-lookup"><span data-stu-id="1a79a-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="1a79a-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span><span class="sxs-lookup"><span data-stu-id="1a79a-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="1a79a-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span><span class="sxs-lookup"><span data-stu-id="1a79a-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="1a79a-142">It is the first variable defined in that file.</span><span class="sxs-lookup"><span data-stu-id="1a79a-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="1a79a-143">Optional: add public application ports</span><span class="sxs-lookup"><span data-stu-id="1a79a-143">Optional: add public application ports</span></span>
<span data-ttu-id="1a79a-144">You may also want to change the public application ports for the cluster before you deploy it.</span><span class="sxs-lookup"><span data-stu-id="1a79a-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="1a79a-145">By default, the template opens up just two public TCP ports (80 and 8081).</span><span class="sxs-lookup"><span data-stu-id="1a79a-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="1a79a-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span><span class="sxs-lookup"><span data-stu-id="1a79a-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="1a79a-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="1a79a-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="1a79a-148">Open that file and search for `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="1a79a-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="1a79a-149">Each port is associated with three artifacts:</span><span class="sxs-lookup"><span data-stu-id="1a79a-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="1a79a-150">A template variable that defines the TCP port value for the port:</span><span class="sxs-lookup"><span data-stu-id="1a79a-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="1a79a-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span><span class="sxs-lookup"><span data-stu-id="1a79a-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="1a79a-152">The probes are part of the Load Balancer resource.</span><span class="sxs-lookup"><span data-stu-id="1a79a-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="1a79a-153">Here is the probe definition for the first default application port:</span><span class="sxs-lookup"><span data-stu-id="1a79a-153">Here is the probe definition for the first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="1a79a-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span><span class="sxs-lookup"><span data-stu-id="1a79a-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="1a79a-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span><span class="sxs-lookup"><span data-stu-id="1a79a-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="1a79a-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1a79a-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="1a79a-157">Deploy the template by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a79a-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="1a79a-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="1a79a-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span><span class="sxs-lookup"><span data-stu-id="1a79a-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Deploy to Resource Group dialog][3]

<span data-ttu-id="1a79a-161">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span><span class="sxs-lookup"><span data-stu-id="1a79a-161">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="1a79a-162">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-162">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="1a79a-163">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span><span class="sxs-lookup"><span data-stu-id="1a79a-163">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="1a79a-164">Hit the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1a79a-164">Hit the **Save** button.</span></span> <span data-ttu-id="1a79a-165">One parameter does not have a persisted value: the administrative account password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-165">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="1a79a-166">You need to provide a password value when Visual Studio prompts you for one.</span><span class="sxs-lookup"><span data-stu-id="1a79a-166">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="1a79a-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span><span class="sxs-lookup"><span data-stu-id="1a79a-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="1a79a-168">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span><span class="sxs-lookup"><span data-stu-id="1a79a-168">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="1a79a-169">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a79a-169">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="1a79a-170">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span><span class="sxs-lookup"><span data-stu-id="1a79a-170">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="1a79a-171">You can monitor the progress of the deployment process in the Visual Studio output window.</span><span class="sxs-lookup"><span data-stu-id="1a79a-171">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="1a79a-172">Once the template deployment is completed, your new cluster is ready to use!</span><span class="sxs-lookup"><span data-stu-id="1a79a-172">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="1a79a-173">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span><span class="sxs-lookup"><span data-stu-id="1a79a-173">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="1a79a-174">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span><span class="sxs-lookup"><span data-stu-id="1a79a-174">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="1a79a-175">For development machines, "unrestricted" policy is usually acceptable.</span><span class="sxs-lookup"><span data-stu-id="1a79a-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="1a79a-176">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span><span class="sxs-lookup"><span data-stu-id="1a79a-176">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="1a79a-177">This will avoid unnecessary prompts during template deployment.</span><span class="sxs-lookup"><span data-stu-id="1a79a-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="1a79a-178">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span><span class="sxs-lookup"><span data-stu-id="1a79a-178">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="1a79a-179">Click **All settings**, then click **Deployments** on the settings blade.</span><span class="sxs-lookup"><span data-stu-id="1a79a-179">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="1a79a-180">A failed resource-group deployment leaves detailed diagnostic information there.</span><span class="sxs-lookup"><span data-stu-id="1a79a-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="1a79a-181">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span><span class="sxs-lookup"><span data-stu-id="1a79a-181">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="1a79a-182">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="1a79a-182">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1a79a-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a79a-183">Next steps</span></span>
* [<span data-ttu-id="1a79a-184">Learn about setting up Service Fabric cluster using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a79a-184">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="1a79a-185">Learn how to manage and deploy Service Fabric applications using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a79a-185">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png



