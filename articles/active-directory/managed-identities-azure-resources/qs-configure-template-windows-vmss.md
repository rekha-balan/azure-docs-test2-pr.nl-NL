---
title: Configure managed identities for Azure resources on a virtual machine scale set using a template
description: Step-by-step instructions for configuring managed identities for Azure resources on a virtual machine scale set, using an Azure Resource Manager template.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/20/2018
ms.author: daveba
ms.openlocfilehash: 965270969eb89e1a30db3215db08bc2e4886792d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969346"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-azure-virtual-machine-scale-using-a-template"></a><span data-ttu-id="68089-103">Configure managed identities for Azure resources on a Azure virtual machine scale using a template</span><span class="sxs-lookup"><span data-stu-id="68089-103">Configure managed identities for Azure resources on a Azure virtual machine scale using a template</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="68089-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68089-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="68089-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="68089-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="68089-106">In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure virtual machine scale set, using Azure Resource Manager deployment template:</span><span class="sxs-lookup"><span data-stu-id="68089-106">In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure virtual machine scale set, using Azure Resource Manager deployment template:</span></span>
- <span data-ttu-id="68089-107">Enable and disable the system-assigned managed identity on an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-107">Enable and disable the system-assigned managed identity on an Azure virtual machine scale set</span></span>
- <span data-ttu-id="68089-108">Add and remove a user-assigned managed identity on an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-108">Add and remove a user-assigned managed identity on an Azure virtual machine scale set</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68089-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68089-109">Prerequisites</span></span>

- <span data-ttu-id="68089-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="68089-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="68089-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="68089-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="68089-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="68089-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="68089-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="68089-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="68089-114">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="68089-114">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="68089-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.</span></span>
    - <span data-ttu-id="68089-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="68089-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="68089-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span></span>

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="68089-118">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="68089-118">Azure Resource Manager templates</span></span>

<span data-ttu-id="68089-119">As with the Azure portal and scripting, [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="68089-119">As with the Azure portal and scripting, [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span></span> <span data-ttu-id="68089-120">Several options are available for template editing and deployment, both local and portal-based, including:</span><span class="sxs-lookup"><span data-stu-id="68089-120">Several options are available for template editing and deployment, both local and portal-based, including:</span></span>

   - <span data-ttu-id="68089-121">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="68089-121">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span></span>
   - <span data-ttu-id="68089-122">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span><span class="sxs-lookup"><span data-stu-id="68089-122">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span></span>
   - <span data-ttu-id="68089-123">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="68089-123">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span></span>
   - <span data-ttu-id="68089-124">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span><span class="sxs-lookup"><span data-stu-id="68089-124">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span></span>  

<span data-ttu-id="68089-125">Regardless of the option you choose, template syntax is the same during initial deployment and redeployment.</span><span class="sxs-lookup"><span data-stu-id="68089-125">Regardless of the option you choose, template syntax is the same during initial deployment and redeployment.</span></span> <span data-ttu-id="68089-126">Enabling managed identities for Azure resources on a new or existing VM is done in the same manner.</span><span class="sxs-lookup"><span data-stu-id="68089-126">Enabling managed identities for Azure resources on a new or existing VM is done in the same manner.</span></span> <span data-ttu-id="68089-127">Also, by default, Azure Resource Manager does an [incremental update](../../azure-resource-manager/deployment-modes.md) to deployments.</span><span class="sxs-lookup"><span data-stu-id="68089-127">Also, by default, Azure Resource Manager does an [incremental update](../../azure-resource-manager/deployment-modes.md) to deployments.</span></span>

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="68089-128">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="68089-128">System-assigned managed identity</span></span>

<span data-ttu-id="68089-129">In this section, you will enable and disable the system-assigned managed identity using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="68089-129">In this section, you will enable and disable the system-assigned managed identity using an Azure Resource Manager template.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-the-creation-of-a-virtual-machines-scale-set-or-a-existing-virtual-machine-scale-set"></a><span data-ttu-id="68089-130">Enable system-assigned managed identity during creation the creation of a virtual machines scale set or a existing virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-130">Enable system-assigned managed identity during creation the creation of a virtual machines scale set or a existing virtual machine scale set</span></span>

1. <span data-ttu-id="68089-131">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-131">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span>
   
2. <span data-ttu-id="68089-132">To enable the system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachinesScaleSets` resource of interest within the resources section and add the `identity` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property.</span><span class="sxs-lookup"><span data-stu-id="68089-132">To enable the system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachinesScaleSets` resource of interest within the resources section and add the `identity` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property.</span></span> <span data-ttu-id="68089-133">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="68089-133">Use the following syntax:</span></span>

   ```JSON
   "identity": { 
       "type": "SystemAssigned"
   }
   ```

3. <span data-ttu-id="68089-134">(Optional) Add the virtual machine scale set managed identities for Azure resources extension as an `extensionsProfile` element.</span><span class="sxs-lookup"><span data-stu-id="68089-134">(Optional) Add the virtual machine scale set managed identities for Azure resources extension as an `extensionsProfile` element.</span></span> <span data-ttu-id="68089-135">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="68089-135">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity, to retrieve tokens as well.</span></span>  <span data-ttu-id="68089-136">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="68089-136">Use the following syntax:</span></span>

   >[!NOTE] 
   > <span data-ttu-id="68089-137">The following example assumes a Windows virtual machine scale set extension (`ManagedIdentityExtensionForWindows`) is being deployed.</span><span class="sxs-lookup"><span data-stu-id="68089-137">The following example assumes a Windows virtual machine scale set extension (`ManagedIdentityExtensionForWindows`) is being deployed.</span></span> <span data-ttu-id="68089-138">You can also configure for Linux by using `ManagedIdentityExtensionForLinux` instead, for the `"name"` and `"type"` elements.</span><span class="sxs-lookup"><span data-stu-id="68089-138">You can also configure for Linux by using `ManagedIdentityExtensionForLinux` instead, for the `"name"` and `"type"` elements.</span></span>
   >

   ```json
   "extensionProfile": {
        "extensions": [
            {
                "name": "ManagedIdentityWindowsExtension",
                "properties": {
                    "publisher": "Microsoft.ManagedIdentity",
                    "type": "ManagedIdentityExtensionForWindows",
                    "typeHandlerVersion": "1.0",
                    "autoUpgradeMinorVersion": true,
                    "settings": {
                        "port": 50342
                    },
                    "protectedSettings": {}
                }
            }
   ```

4. <span data-ttu-id="68089-139">When you're done, the following sections should added to the resource section of your template  and should resemble the following:</span><span class="sxs-lookup"><span data-stu-id="68089-139">When you're done, the following sections should added to the resource section of your template  and should resemble the following:</span></span>

   ```json
    "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "SystemAssigned",
            },
           "properties": {
                //other resource provider properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ``` 

### <a name="disable-a-system-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="68089-140">Disable a system-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-140">Disable a system-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="68089-141">If you have a virtual machine scale set that no longer needs a system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="68089-141">If you have a virtual machine scale set that no longer needs a system-assigned managed identity:</span></span>

1. <span data-ttu-id="68089-142">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-142">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span>

2. <span data-ttu-id="68089-143">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section.</span><span class="sxs-lookup"><span data-stu-id="68089-143">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section.</span></span> <span data-ttu-id="68089-144">If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.</span><span class="sxs-lookup"><span data-stu-id="68089-144">If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.</span></span>

   <span data-ttu-id="68089-145">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="68089-145">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span></span>

   <span data-ttu-id="68089-146">If your apiVersion is `2018-06-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the userAssignedIdentities dictionary values.</span><span class="sxs-lookup"><span data-stu-id="68089-146">If your apiVersion is `2018-06-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the userAssignedIdentities dictionary values.</span></span>

   <span data-ttu-id="68089-147">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="68089-147">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01 and earlier**</span></span>

   <span data-ttu-id="68089-148">If your apiVersion is `2017-12-01` and your virtual machine scale set has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="68089-148">If your apiVersion is `2017-12-01` and your virtual machine scale set has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.</span></span> 
   
    

   <span data-ttu-id="68089-149">The following example shows you how remove a system-assigned managed identity from a virtual machine scale set with no user-assigned managed identities:</span><span class="sxs-lookup"><span data-stu-id="68089-149">The following example shows you how remove a system-assigned managed identity from a virtual machine scale set with no user-assigned managed identities:</span></span>
   
   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "None"
        }

   }
   ```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="68089-150">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="68089-150">User-assigned managed identity</span></span>

<span data-ttu-id="68089-151">In this section, you assign a user-assigned managed identity to a virtual machine scale set using Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="68089-151">In this section, you assign a user-assigned managed identity to a virtual machine scale set using Azure Resource Manager template.</span></span>

> [!Note]
> <span data-ttu-id="68089-152">To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).</span><span class="sxs-lookup"><span data-stu-id="68089-152">To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).</span></span>

### <a name="assign-a-user-assigned-managed-identity-to-a-virutal-machine-scale-set"></a><span data-ttu-id="68089-153">Assign a user-assigned managed identity to a virutal machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-153">Assign a user-assigned managed identity to a virutal machine scale set</span></span>

1. <span data-ttu-id="68089-154">Under the `resources` element, add the following entry to assign a user-assigned managed identity to your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-154">Under the `resources` element, add the following entry to assign a user-assigned managed identity to your virtual machine scale set.</span></span>  <span data-ttu-id="68089-155">Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.</span><span class="sxs-lookup"><span data-stu-id="68089-155">Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.</span></span>
   
   <span data-ttu-id="68089-156">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="68089-156">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span></span>

   <span data-ttu-id="68089-157">If your apiVersion is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span><span class="sxs-lookup"><span data-stu-id="68089-157">If your apiVersion is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span></span>

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "userAssigned",
           "userAssignedIdentities": {
               "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
           }
       }
    
   }
   ```   

   <span data-ttu-id="68089-158">**Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**</span><span class="sxs-lookup"><span data-stu-id="68089-158">**Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**</span></span>
    
   <span data-ttu-id="68089-159">If your `apiVersion` is `2017-12-01` or earlier, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the variables section of your template.</span><span class="sxs-lookup"><span data-stu-id="68089-159">If your `apiVersion` is `2017-12-01` or earlier, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the variables section of your template.</span></span>

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2017-03-30",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "userAssigned",
           "identityIds": [
               "[resourceID('Micrososft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITY>'))]"
           ]
       }

   }
   ``` 

2. <span data-ttu-id="68089-160">(Optional) Add the following entry under the `extensionProfile` element to assign the managed identities for Azure resources extension to your VMSS.</span><span class="sxs-lookup"><span data-stu-id="68089-160">(Optional) Add the following entry under the `extensionProfile` element to assign the managed identities for Azure resources extension to your VMSS.</span></span> <span data-ttu-id="68089-161">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="68089-161">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span> <span data-ttu-id="68089-162">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="68089-162">Use the following syntax:</span></span>
   
    ```JSON
       "extensionProfile": {
            "extensions": [
                {
                    "name": "ManagedIdentityWindowsExtension",
                    "properties": {
                        "publisher": "Microsoft.ManagedIdentity",
                        "type": "ManagedIdentityExtensionForWindows",
                        "typeHandlerVersion": "1.0",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "port": 50342
                        },
                        "protectedSettings": {}
                    }
                }
    ```

3. <span data-ttu-id="68089-163">When you are done, your template should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="68089-163">When you are done, your template should look similar to the following:</span></span>
   
   <span data-ttu-id="68089-164">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="68089-164">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span></span>   

   ```json
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "UserAssigned",
                "userAssignedIdentities": {
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
                }
            },
           "properties": {
                //other virtual machine properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ```

   <span data-ttu-id="68089-165">**Microsoft.Compute/virtualMachines API version 2017-12-01 eand earlier**</span><span class="sxs-lookup"><span data-stu-id="68089-165">**Microsoft.Compute/virtualMachines API version 2017-12-01 eand earlier**</span></span>

   ```json
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2017-12-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "UserAssigned",
                "identityIds": [
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
                ]
            },
           "properties": {
                //other virtual machine properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ```
### <a name="remove-user-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="68089-166">Remove user-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="68089-166">Remove user-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="68089-167">If you have a virtual machine scale set that no longer needs a user-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="68089-167">If you have a virtual machine scale set that no longer needs a user-assigned managed identity:</span></span>

1. <span data-ttu-id="68089-168">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="68089-168">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span>

2. <span data-ttu-id="68089-169">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section.</span><span class="sxs-lookup"><span data-stu-id="68089-169">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section.</span></span> <span data-ttu-id="68089-170">If you have a virtual machine scale set that only has user-assigned managed identity, you can disable it by changing the the identity type to `None`.</span><span class="sxs-lookup"><span data-stu-id="68089-170">If you have a virtual machine scale set that only has user-assigned managed identity, you can disable it by changing the the identity type to `None`.</span></span>

   <span data-ttu-id="68089-171">The following example shows you how remove all user-assigned managed identities from a VM with no system-assigned managed identities:</span><span class="sxs-lookup"><span data-stu-id="68089-171">The following example shows you how remove all user-assigned managed identities from a VM with no system-assigned managed identities:</span></span>

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "None"
        }
   }
   ```
   
   <span data-ttu-id="68089-172">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="68089-172">**Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**</span></span>
    
   <span data-ttu-id="68089-173">To remove a a single user-assigned managed identity from a virtual machine scale set, remove it from the `userAssignedIdentities` dictionary.</span><span class="sxs-lookup"><span data-stu-id="68089-173">To remove a a single user-assigned managed identity from a virtual machine scale set, remove it from the `userAssignedIdentities` dictionary.</span></span>

   <span data-ttu-id="68089-174">If you have a system-assigned identity, keep it in the in the `type` value under the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="68089-174">If you have a system-assigned identity, keep it in the in the `type` value under the `identity` value.</span></span>

   <span data-ttu-id="68089-175">**Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**</span><span class="sxs-lookup"><span data-stu-id="68089-175">**Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**</span></span>

   <span data-ttu-id="68089-176">To remove a single user-assigned managed identity from a virtual machine scale set, remove it from the `identityIds` array.</span><span class="sxs-lookup"><span data-stu-id="68089-176">To remove a single user-assigned managed identity from a virtual machine scale set, remove it from the `identityIds` array.</span></span>

   <span data-ttu-id="68089-177">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="68089-177">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="68089-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="68089-178">Next steps</span></span>

- <span data-ttu-id="68089-179">[Managed identities for Azure resources overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="68089-179">[Managed identities for Azure resources overview](overview.md).</span></span>

