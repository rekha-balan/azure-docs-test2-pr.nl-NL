---
title: Configure the roles for an Azure cloud service with Visual Studio | Microsoft Docs
description: Learn how to set up and configure roles for Azure cloud services using Visual Studio.
services: visual-studio-online
author: ghogen
manager: douge
assetId: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 010a345d0bc756855b9a85660afcd647d111db75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801104"
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="fcc56-103">Configure Azure cloud service roles with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcc56-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="fcc56-104">An Azure cloud service can have one or more worker or web roles.</span><span class="sxs-lookup"><span data-stu-id="fcc56-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="fcc56-105">For each role, you need to define how that role is set up and also configure how that role runs.</span><span class="sxs-lookup"><span data-stu-id="fcc56-105">For each role, you need to define how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="fcc56-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="fcc56-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="fcc56-107">The information for your cloud service is stored in the following files:</span><span class="sxs-lookup"><span data-stu-id="fcc56-107">The information for your cloud service is stored in the following files:</span></span>

- <span data-ttu-id="fcc56-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span><span class="sxs-lookup"><span data-stu-id="fcc56-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="fcc56-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span><span class="sxs-lookup"><span data-stu-id="fcc56-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="fcc56-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span><span class="sxs-lookup"><span data-stu-id="fcc56-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span></span> <span data-ttu-id="fcc56-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span><span class="sxs-lookup"><span data-stu-id="fcc56-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="fcc56-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="fcc56-113">You can use a different service configuration for each deployment environment.</span><span class="sxs-lookup"><span data-stu-id="fcc56-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="fcc56-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span><span class="sxs-lookup"><span data-stu-id="fcc56-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span></span>

<span data-ttu-id="fcc56-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span><span class="sxs-lookup"><span data-stu-id="fcc56-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="fcc56-116">Configure an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="fcc56-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="fcc56-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span><span class="sxs-lookup"><span data-stu-id="fcc56-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span></span>

1. <span data-ttu-id="fcc56-118">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcc56-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fcc56-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
    ![Solution Explorer project context menu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="fcc56-121">In the project's properties page, select the **Development** tab.</span><span class="sxs-lookup"><span data-stu-id="fcc56-121">In the project's properties page, select the **Development** tab.</span></span> 

    ![Project properties page - development tab](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="fcc56-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="fcc56-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span></span> <span data-ttu-id="fcc56-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span><span class="sxs-lookup"><span data-stu-id="fcc56-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="fcc56-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="fcc56-126">To edit these properties, you must select **All Configurations**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-126">To edit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Service Configuration list for an Azure cloud service](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a><span data-ttu-id="fcc56-128">Change the number of role instances</span><span class="sxs-lookup"><span data-stu-id="fcc56-128">Change the number of role instances</span></span>
<span data-ttu-id="fcc56-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span><span class="sxs-lookup"><span data-stu-id="fcc56-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span></span> <span data-ttu-id="fcc56-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span></span> <span data-ttu-id="fcc56-131">This affects the billing for the deployment of this cloud service.</span><span class="sxs-lookup"><span data-stu-id="fcc56-131">This affects the billing for the deployment of this cloud service.</span></span> <span data-ttu-id="fcc56-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="fcc56-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="fcc56-133">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcc56-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fcc56-134">In **Solution Explorer**, expand the project node.</span><span class="sxs-lookup"><span data-stu-id="fcc56-134">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="fcc56-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure role context menu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="fcc56-137">Select the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="fcc56-137">Select the **Configuration** tab.</span></span>

    ![Configuration tab](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="fcc56-139">In the **Service Configuration** list, select the service configuration that you want to update.</span><span class="sxs-lookup"><span data-stu-id="fcc56-139">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>
   
    ![Service Configuration list](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="fcc56-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span><span class="sxs-lookup"><span data-stu-id="fcc56-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span></span> <span data-ttu-id="fcc56-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span></span>

    ![Updating the Instance Count](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="fcc56-144">From the Visual Studio, toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-144">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="fcc56-145">Manage connection strings for storage accounts</span><span class="sxs-lookup"><span data-stu-id="fcc56-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="fcc56-146">You can add, remove, or modify connection strings for your service configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="fcc56-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="fcc56-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="fcc56-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="fcc56-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="fcc56-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span></span> <span data-ttu-id="fcc56-150">However, this information is currently not stored as encrypted text.</span><span class="sxs-lookup"><span data-stu-id="fcc56-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="fcc56-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="fcc56-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span><span class="sxs-lookup"><span data-stu-id="fcc56-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="fcc56-153">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcc56-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fcc56-154">In **Solution Explorer**, expand the project node.</span><span class="sxs-lookup"><span data-stu-id="fcc56-154">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="fcc56-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure role context menu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="fcc56-157">Select the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="fcc56-157">Select the **Settings** tab.</span></span>

    ![Settings tab](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="fcc56-159">In the **Service Configuration** list, select the service configuration that you want to update.</span><span class="sxs-lookup"><span data-stu-id="fcc56-159">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Service Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="fcc56-161">To add a connection string, select **Add Setting**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-161">To add a connection string, select **Add Setting**.</span></span>

    ![Add connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="fcc56-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span><span class="sxs-lookup"><span data-stu-id="fcc56-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="fcc56-165">**Name** - Enter the name that you want to use for the connection string.</span><span class="sxs-lookup"><span data-stu-id="fcc56-165">**Name** - Enter the name that you want to use for the connection string.</span></span>
    - <span data-ttu-id="fcc56-166">**Type** - Select **Connection String** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="fcc56-166">**Type** - Select **Connection String** from the drop-down list.</span></span>
    - <span data-ttu-id="fcc56-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span><span class="sxs-lookup"><span data-stu-id="fcc56-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="fcc56-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="fcc56-169">Then follow the instructions for the option you select:</span><span class="sxs-lookup"><span data-stu-id="fcc56-169">Then follow the instructions for the option you select:</span></span>

    - <span data-ttu-id="fcc56-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span></span> <span data-ttu-id="fcc56-171">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-171">Select **OK**.</span></span>
    - <span data-ttu-id="fcc56-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="fcc56-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="fcc56-173">Select an Azure subscription and storage account.</span><span class="sxs-lookup"><span data-stu-id="fcc56-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="fcc56-174">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-174">Select **OK**.</span></span>
    - <span data-ttu-id="fcc56-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span><span class="sxs-lookup"><span data-stu-id="fcc56-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span></span> <span data-ttu-id="fcc56-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="fcc56-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="fcc56-178">From the Visual Studio, toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-178">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="fcc56-179">Programmatically access a connection string</span><span class="sxs-lookup"><span data-stu-id="fcc56-179">Programmatically access a connection string</span></span>

<span data-ttu-id="fcc56-180">The following steps show how to programmatically access a connection string using C#.</span><span class="sxs-lookup"><span data-stu-id="fcc56-180">The following steps show how to programmatically access a connection string using C#.</span></span>

1. <span data-ttu-id="fcc56-181">Add the following using directives to a C# file where you are going to use the setting:</span><span class="sxs-lookup"><span data-stu-id="fcc56-181">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="fcc56-182">The following code illustrates an example of how to access a connection string.</span><span class="sxs-lookup"><span data-stu-id="fcc56-182">The following code illustrates an example of how to access a connection string.</span></span> <span data-ttu-id="fcc56-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span><span class="sxs-lookup"><span data-stu-id="fcc56-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a><span data-ttu-id="fcc56-184">Add custom settings to use in your Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="fcc56-184">Add custom settings to use in your Azure cloud service</span></span>
<span data-ttu-id="fcc56-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span><span class="sxs-lookup"><span data-stu-id="fcc56-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="fcc56-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span><span class="sxs-lookup"><span data-stu-id="fcc56-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span></span> <span data-ttu-id="fcc56-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span><span class="sxs-lookup"><span data-stu-id="fcc56-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="fcc56-188">Your code can check for notifications of when a setting changes.</span><span class="sxs-lookup"><span data-stu-id="fcc56-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="fcc56-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcc56-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="fcc56-190">You can add, remove, or modify custom settings for your service configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="fcc56-191">You might want different values for these strings for different service configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="fcc56-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc56-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="fcc56-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span><span class="sxs-lookup"><span data-stu-id="fcc56-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="fcc56-194">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcc56-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fcc56-195">In **Solution Explorer**, expand the project node.</span><span class="sxs-lookup"><span data-stu-id="fcc56-195">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="fcc56-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure role context menu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="fcc56-198">Select the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="fcc56-198">Select the **Settings** tab.</span></span>

    ![Settings tab](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="fcc56-200">In the **Service Configuration** list, select the service configuration that you want to update.</span><span class="sxs-lookup"><span data-stu-id="fcc56-200">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Service Configuration list](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="fcc56-202">To add a custom setting, select **Add Setting**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-202">To add a custom setting, select **Add Setting**.</span></span>

    ![Add custom setting](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="fcc56-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span><span class="sxs-lookup"><span data-stu-id="fcc56-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![New custom setting](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="fcc56-206">**Name** - Enter the name of the setting.</span><span class="sxs-lookup"><span data-stu-id="fcc56-206">**Name** - Enter the name of the setting.</span></span>
    - <span data-ttu-id="fcc56-207">**Type** - Select **String** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="fcc56-207">**Type** - Select **String** from the drop-down list.</span></span>
    - <span data-ttu-id="fcc56-208">**Value** - Enter the value of the setting.</span><span class="sxs-lookup"><span data-stu-id="fcc56-208">**Value** - Enter the value of the setting.</span></span> <span data-ttu-id="fcc56-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span><span class="sxs-lookup"><span data-stu-id="fcc56-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span></span>  

1. <span data-ttu-id="fcc56-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="fcc56-211">From the Visual Studio, toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-211">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="fcc56-212">Programmatically access a custom setting's value</span><span class="sxs-lookup"><span data-stu-id="fcc56-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="fcc56-213">The following steps show how to programmatically access a custom setting using C#.</span><span class="sxs-lookup"><span data-stu-id="fcc56-213">The following steps show how to programmatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="fcc56-214">Add the following using directives to a C# file where you are going to use the setting:</span><span class="sxs-lookup"><span data-stu-id="fcc56-214">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="fcc56-215">The following code illustrates an example of how to access a custom setting.</span><span class="sxs-lookup"><span data-stu-id="fcc56-215">The following code illustrates an example of how to access a custom setting.</span></span> <span data-ttu-id="fcc56-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span><span class="sxs-lookup"><span data-stu-id="fcc56-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="fcc56-217">Manage local storage for each role instance</span><span class="sxs-lookup"><span data-stu-id="fcc56-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="fcc56-218">You can add local file system storage for each instance of a role.</span><span class="sxs-lookup"><span data-stu-id="fcc56-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="fcc56-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span><span class="sxs-lookup"><span data-stu-id="fcc56-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="fcc56-220">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcc56-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fcc56-221">In **Solution Explorer**, expand the project node.</span><span class="sxs-lookup"><span data-stu-id="fcc56-221">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="fcc56-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Solution Explorer Azure role context menu](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="fcc56-224">Select the **Local Storage** tab.</span><span class="sxs-lookup"><span data-stu-id="fcc56-224">Select the **Local Storage** tab.</span></span>

    ![Local storage tab](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="fcc56-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span><span class="sxs-lookup"><span data-stu-id="fcc56-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span></span> <span data-ttu-id="fcc56-227">Any other value results in all the input fields on the page being disabled.</span><span class="sxs-lookup"><span data-stu-id="fcc56-227">Any other value results in all the input fields on the page being disabled.</span></span> 

    ![Service Configuration list](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="fcc56-229">To add a local storage entry, select **Add Local Storage**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-229">To add a local storage entry, select **Add Local Storage**.</span></span>

    ![Add local storage](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="fcc56-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span><span class="sxs-lookup"><span data-stu-id="fcc56-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span></span>

    ![New local storage entry](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="fcc56-233">**Name** - Enter the name that you want to use for the new local storage.</span><span class="sxs-lookup"><span data-stu-id="fcc56-233">**Name** - Enter the name that you want to use for the new local storage.</span></span>
    - <span data-ttu-id="fcc56-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span><span class="sxs-lookup"><span data-stu-id="fcc56-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span></span>
    - <span data-ttu-id="fcc56-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span><span class="sxs-lookup"><span data-stu-id="fcc56-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span></span>

1. <span data-ttu-id="fcc56-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="fcc56-237">From the Visual Studio, toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-237">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="fcc56-238">Programmatically accessing local storage</span><span class="sxs-lookup"><span data-stu-id="fcc56-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="fcc56-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="fcc56-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-to-local-storage"></a><span data-ttu-id="fcc56-240">Write a text file to local storage</span><span class="sxs-lookup"><span data-stu-id="fcc56-240">Write a text file to local storage</span></span>

<span data-ttu-id="fcc56-241">The following code shows an example of how to write a text file to local storage.</span><span class="sxs-lookup"><span data-stu-id="fcc56-241">The following code shows an example of how to write a text file to local storage.</span></span> <span data-ttu-id="fcc56-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span><span class="sxs-lookup"><span data-stu-id="fcc56-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a><span data-ttu-id="fcc56-243">Find a file written to local storage</span><span class="sxs-lookup"><span data-stu-id="fcc56-243">Find a file written to local storage</span></span>

<span data-ttu-id="fcc56-244">To view the file created by the code in the previous section, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="fcc56-244">To view the file created by the code in the previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="fcc56-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Show Azure compute emulator](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="fcc56-247">Select the web role.</span><span class="sxs-lookup"><span data-stu-id="fcc56-247">Select the web role.</span></span>

    ![Azure compute emulator](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="fcc56-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span><span class="sxs-lookup"><span data-stu-id="fcc56-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Open local store menu item](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="fcc56-251">When the Windows Explorer window opens, enter \`MyLocalStorageTest.txt\`\` into the **Search** text box, and select **Enter** to start the search.</span><span class="sxs-lookup"><span data-stu-id="fcc56-251">When the Windows Explorer window opens, enter \`MyLocalStorageTest.txt\`\` into the **Search** text box, and select **Enter** to start the search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fcc56-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="fcc56-252">Next steps</span></span>
<span data-ttu-id="fcc56-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="fcc56-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="fcc56-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="fcc56-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

