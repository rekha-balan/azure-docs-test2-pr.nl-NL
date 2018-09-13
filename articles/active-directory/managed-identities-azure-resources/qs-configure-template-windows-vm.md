---
title: How to configure managed identities for Azure resources on an Azure VM by using a template
description: Step-by-step instructions for configuring managed identities for Azure resources on an Azure VM, using an Azure Resource Manager template.
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
ms.date: 09/14/2017
ms.author: daveba
ms.openlocfilehash: e4b355fef27414faa0fadd618d975c2b5672f360
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967716"
---
# <a name="configure-managed-identities-for-azure-resources-on-an-azure-vm-using-a-templates"></a><span data-ttu-id="749c0-103">Configure managed identities for Azure resources on an Azure VM using a templates</span><span class="sxs-lookup"><span data-stu-id="749c0-103">Configure managed identities for Azure resources on an Azure VM using a templates</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="749c0-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="749c0-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="749c0-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="749c0-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="749c0-106">In this article, using the Azure Resource Manager deployment template, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span><span class="sxs-lookup"><span data-stu-id="749c0-106">In this article, using the Azure Resource Manager deployment template, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span></span>

## <a name="prerequisites"></a><span data-ttu-id="749c0-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="749c0-107">Prerequisites</span></span>

- <span data-ttu-id="749c0-108">If you're unfamiliar with using Azure Resource Manager deployment template, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="749c0-108">If you're unfamiliar with using Azure Resource Manager deployment template, check out the [overview section](overview.md).</span></span> <span data-ttu-id="749c0-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="749c0-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="749c0-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="749c0-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="749c0-111">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="749c0-111">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="749c0-112">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="749c0-112">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="749c0-113">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-113">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span></span>
    - <span data-ttu-id="749c0-114">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="749c0-114">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="749c0-115">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-115">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span></span>

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="749c0-116">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="749c0-116">Azure Resource Manager templates</span></span>

<span data-ttu-id="749c0-117">As with the Azure portal and scripting, [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="749c0-117">As with the Azure portal and scripting, [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span></span> <span data-ttu-id="749c0-118">Several options are available for template editing and deployment, both local and portal-based, including:</span><span class="sxs-lookup"><span data-stu-id="749c0-118">Several options are available for template editing and deployment, both local and portal-based, including:</span></span>

   - <span data-ttu-id="749c0-119">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="749c0-119">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span></span>
   - <span data-ttu-id="749c0-120">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span><span class="sxs-lookup"><span data-stu-id="749c0-120">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span></span>
   - <span data-ttu-id="749c0-121">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="749c0-121">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span></span>
   - <span data-ttu-id="749c0-122">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span><span class="sxs-lookup"><span data-stu-id="749c0-122">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span></span>  

<span data-ttu-id="749c0-123">Regardless of the option you choose, template syntax is the same during initial deployment and redeployment.</span><span class="sxs-lookup"><span data-stu-id="749c0-123">Regardless of the option you choose, template syntax is the same during initial deployment and redeployment.</span></span> <span data-ttu-id="749c0-124">Enabling a system or user-assigned managed identity on a new or existing VM is done in the same manner.</span><span class="sxs-lookup"><span data-stu-id="749c0-124">Enabling a system or user-assigned managed identity on a new or existing VM is done in the same manner.</span></span> <span data-ttu-id="749c0-125">Also, by default, Azure Resource Manager does an [incremental update](../../azure-resource-manager/deployment-modes.md) to deployments.</span><span class="sxs-lookup"><span data-stu-id="749c0-125">Also, by default, Azure Resource Manager does an [incremental update](../../azure-resource-manager/deployment-modes.md) to deployments.</span></span>

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="749c0-126">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="749c0-126">System-assigned managed identity</span></span>

<span data-ttu-id="749c0-127">In this section, you will enable and disable a system-assigned managed identity using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="749c0-127">In this section, you will enable and disable a system-assigned managed identity using an Azure Resource Manager template.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-an-azure-vm-or-on-an-existing-vm"></a><span data-ttu-id="749c0-128">Enable system-assigned managed identity during creation of an Azure VM or on an existing VM</span><span class="sxs-lookup"><span data-stu-id="749c0-128">Enable system-assigned managed identity during creation of an Azure VM or on an existing VM</span></span>

1. <span data-ttu-id="749c0-129">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-129">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span></span>

2. <span data-ttu-id="749c0-130">To enable system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section and add the `"identity"` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property.</span><span class="sxs-lookup"><span data-stu-id="749c0-130">To enable system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section and add the `"identity"` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property.</span></span> <span data-ttu-id="749c0-131">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="749c0-131">Use the following syntax:</span></span>

   ```JSON
   "identity": { 
       "type": "SystemAssigned"
   },
   ```

3. <span data-ttu-id="749c0-132">(Optional) Add the VM managed identities for Azure resources extension as a `resources` element.</span><span class="sxs-lookup"><span data-stu-id="749c0-132">(Optional) Add the VM managed identities for Azure resources extension as a `resources` element.</span></span> <span data-ttu-id="749c0-133">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="749c0-133">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span>  <span data-ttu-id="749c0-134">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="749c0-134">Use the following syntax:</span></span>

   >[!NOTE] 
   > <span data-ttu-id="749c0-135">The following example assumes a Windows VM extension (`ManagedIdentityExtensionForWindows`) is being deployed.</span><span class="sxs-lookup"><span data-stu-id="749c0-135">The following example assumes a Windows VM extension (`ManagedIdentityExtensionForWindows`) is being deployed.</span></span> <span data-ttu-id="749c0-136">You can also configure for Linux by using `ManagedIdentityExtensionForLinux` instead, for the `"name"` and `"type"` elements.</span><span class="sxs-lookup"><span data-stu-id="749c0-136">You can also configure for Linux by using `ManagedIdentityExtensionForLinux` instead, for the `"name"` and `"type"` elements.</span></span> <span data-ttu-id="749c0-137">The VM extension is planned for deprecation in January 2019.</span><span class="sxs-lookup"><span data-stu-id="749c0-137">The VM extension is planned for deprecation in January 2019.</span></span>
   >

   ```JSON
   { 
       "type": "Microsoft.Compute/virtualMachines/extensions",
       "name": "[concat(variables('vmName'),'/ManagedIdentityExtensionForWindows')]",
       "apiVersion": "2018-06-01",
       "location": "[resourceGroup().location]",
       "dependsOn": [
           "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
       ],
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

4. <span data-ttu-id="749c0-138">When you're done, the following sections should added to the `resource` section of your template and it should resemble the following:</span><span class="sxs-lookup"><span data-stu-id="749c0-138">When you're done, the following sections should added to the `resource` section of your template and it should resemble the following:</span></span>

   ```JSON
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[variables('vmName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "SystemAssigned",
                },
            },
            {
            "type": "Microsoft.Compute/virtualMachines/extensions",
            "name": "[concat(variables('vmName'),'/ManagedIdentityExtensionForLinux')]",
            "apiVersion": "2018-06-01",
            "location": "[resourceGroup().location]",
            "dependsOn": [
                "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
            ],
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
   ```

### <a name="assign-a-role-the-vms-system-assigned-managed-identity"></a><span data-ttu-id="749c0-139">Assign a role the VM's system-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="749c0-139">Assign a role the VM's system-assigned managed identity</span></span>

<span data-ttu-id="749c0-140">After you have enabled system-assigned managed identity on your VM, you may want to grant it a role such as **Reader** access to the resource group in which it was created.</span><span class="sxs-lookup"><span data-stu-id="749c0-140">After you have enabled system-assigned managed identity on your VM, you may want to grant it a role such as **Reader** access to the resource group in which it was created.</span></span>

1. <span data-ttu-id="749c0-141">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-141">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span></span>
 
2. <span data-ttu-id="749c0-142">Load the template into an [editor](#azure-resource-manager-templates) and add the following information to give your VM **Reader** access to the resource group in which it was created.</span><span class="sxs-lookup"><span data-stu-id="749c0-142">Load the template into an [editor](#azure-resource-manager-templates) and add the following information to give your VM **Reader** access to the resource group in which it was created.</span></span>  <span data-ttu-id="749c0-143">Your template structure may vary depending on the editor and the deployment model you choose.</span><span class="sxs-lookup"><span data-stu-id="749c0-143">Your template structure may vary depending on the editor and the deployment model you choose.</span></span>
   
   <span data-ttu-id="749c0-144">Under the `parameters` section add the following:</span><span class="sxs-lookup"><span data-stu-id="749c0-144">Under the `parameters` section add the following:</span></span>

    ```JSON
    "builtInRoleType": {
          "type": "string",
          "defaultValue": "Reader"
        },
        "rbacGuid": {
          "type": "string"
        }
    ```

    <span data-ttu-id="749c0-145">Under the `variables` section add the following:</span><span class="sxs-lookup"><span data-stu-id="749c0-145">Under the `variables` section add the following:</span></span>

    ```JSON
    "Reader": "[concat('/subscriptions/', subscription().subscriptionId, '/providers/Microsoft.Authorization/roleDefinitions/', 'acdd72a7-3385-48ef-bd42-f606fba81ae7')]"
    ```

    <span data-ttu-id="749c0-146">Under the `resources` section add the following:</span><span class="sxs-lookup"><span data-stu-id="749c0-146">Under the `resources` section add the following:</span></span>

    ```JSON
    {
        "apiVersion": "2017-09-01",
         "type": "Microsoft.Authorization/roleAssignments",
         "name": "[parameters('rbacGuid')]",
         "properties": {
                "roleDefinitionId": "[variables(parameters('builtInRoleType'))]",
                "principalId": "[reference(variables('vmResourceId'), '2017-12-01', 'Full').identity.principalId]",
                "scope": "[resourceGroup().id]"
          },
          "dependsOn": [
                "[concat('Microsoft.Compute/virtualMachines/', parameters('vmName'))]"
            ]
    }
    ```

### <a name="disable-a-system-assigned-managed-identity-from-an-azure-vm"></a><span data-ttu-id="749c0-147">Disable a system-assigned managed identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="749c0-147">Disable a system-assigned managed identity from an Azure VM</span></span>

<span data-ttu-id="749c0-148">If you have a VM that no longer needs a system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="749c0-148">If you have a VM that no longer needs a system-assigned managed identity:</span></span>

1. <span data-ttu-id="749c0-149">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-149">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span></span>

2. <span data-ttu-id="749c0-150">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section.</span><span class="sxs-lookup"><span data-stu-id="749c0-150">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section.</span></span> <span data-ttu-id="749c0-151">If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.</span><span class="sxs-lookup"><span data-stu-id="749c0-151">If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.</span></span>  
   
   <span data-ttu-id="749c0-152">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="749c0-152">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span></span>

   <span data-ttu-id="749c0-153">If your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `userAssignedIdentities` dictionary values.</span><span class="sxs-lookup"><span data-stu-id="749c0-153">If your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `userAssignedIdentities` dictionary values.</span></span>

   <span data-ttu-id="749c0-154">**Microsoft.Compute/virtualMachines API version 2018-06-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="749c0-154">**Microsoft.Compute/virtualMachines API version 2018-06-01 and earlier**</span></span>
   
   <span data-ttu-id="749c0-155">If your `apiVersion` is `2017-12-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="749c0-155">If your `apiVersion` is `2017-12-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.</span></span>  
   
<span data-ttu-id="749c0-156">The following example shows you how remove a system-assigned managed identity from a VM with no user-assigned managed identities:</span><span class="sxs-lookup"><span data-stu-id="749c0-156">The following example shows you how remove a system-assigned managed identity from a VM with no user-assigned managed identities:</span></span>

```JSON
{
    "apiVersion": "2018-06-01",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[parameters('vmName')]",
    "location": "[resourceGroup().location]",
    "identity": { 
        "type": "None"
}
```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="749c0-157">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="749c0-157">User-assigned managed identity</span></span>

<span data-ttu-id="749c0-158">In this section, you assign a user-assigned managed identity to an Azure VM using Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="749c0-158">In this section, you assign a user-assigned managed identity to an Azure VM using Azure Resource Manager template.</span></span>

> [!Note]
> <span data-ttu-id="749c0-159">To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).</span><span class="sxs-lookup"><span data-stu-id="749c0-159">To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).</span></span>

 ### <a name="assign-a-user-assigned-managed-identity-to-an-azure-vm"></a><span data-ttu-id="749c0-160">Assign a user-assigned managed identity to an Azure VM</span><span class="sxs-lookup"><span data-stu-id="749c0-160">Assign a user-assigned managed identity to an Azure VM</span></span>

1. <span data-ttu-id="749c0-161">Under the `resources` element, add the following entry to assign a user-assigned managed identity to your VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-161">Under the `resources` element, add the following entry to assign a user-assigned managed identity to your VM.</span></span>  <span data-ttu-id="749c0-162">Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.</span><span class="sxs-lookup"><span data-stu-id="749c0-162">Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.</span></span>

   <span data-ttu-id="749c0-163">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="749c0-163">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span></span>

   <span data-ttu-id="749c0-164">If your `apiVersion` is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span><span class="sxs-lookup"><span data-stu-id="749c0-164">If your `apiVersion` is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span></span>

   ```json
   {
       "apiVersion": "2018-06-01",
       "type": "Microsoft.Compute/virtualMachines",
       "name": "[variables('vmName')]",
       "location": "[resourceGroup().location]",
       "identity": {
           "type": "userAssigned",
           "userAssignedIdentities": {
               "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
           }
        }
   }
   ```
   
   <span data-ttu-id="749c0-165">**Microsoft.Compute/virtualMachines API version 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="749c0-165">**Microsoft.Compute/virtualMachines API version 2017-12-01 and earlier**</span></span>
    
   <span data-ttu-id="749c0-166">If your `apiVersion` is `2017-12-01`, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span><span class="sxs-lookup"><span data-stu-id="749c0-166">If your `apiVersion` is `2017-12-01`, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.</span></span>
    
   ```json
   {
       "apiVersion": "2017-12-01",
       "type": "Microsoft.Compute/virtualMachines",
       "name": "[variables('vmName')]",
       "location": "[resourceGroup().location]",
       "identity": {
           "type": "userAssigned",
           "identityIds": [
               "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
           ]
       }
   }
   ```
       

2. <span data-ttu-id="749c0-167">(Optional) Next, under the `resources` element, add the following entry to assign the managed identity extension to your VM (planned for deprecation in January 2019).</span><span class="sxs-lookup"><span data-stu-id="749c0-167">(Optional) Next, under the `resources` element, add the following entry to assign the managed identity extension to your VM (planned for deprecation in January 2019).</span></span> <span data-ttu-id="749c0-168">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="749c0-168">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span> <span data-ttu-id="749c0-169">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="749c0-169">Use the following syntax:</span></span>
    ```json
    {
        "type": "Microsoft.Compute/virtualMachines/extensions",
        "name": "[concat(variables('vmName'),'/ManagedIdentityExtensionForWindows')]",
        "apiVersion": "2018-06-01",
        "location": "[resourceGroup().location]",
        "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
        ],
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
    ```
    
3. <span data-ttu-id="749c0-170">When you're done, the following sections should added to the `resource` section of your template and it should resemble the following:</span><span class="sxs-lookup"><span data-stu-id="749c0-170">When you're done, the following sections should added to the `resource` section of your template and it should resemble the following:</span></span>
   
   <span data-ttu-id="749c0-171">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="749c0-171">**Microsoft.Compute/virtualMachines API version 2018-06-01**</span></span>    

   ```JSON
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[variables('vmName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "userAssigned",
                "userAssignedIdentities": {
                   "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
                }
            }
        },
        {
            "type": "Microsoft.Compute/virtualMachines/extensions",
            "name": "[concat(variables('vmName'),'/ManagedIdentityExtensionForLinux')]",
            "apiVersion": "2018-06-01-preview",
            "location": "[resourceGroup().location]",
            "dependsOn": [
                "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
            ],
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
   ```
   <span data-ttu-id="749c0-172">**Microsoft.Compute/virtualMachines API version 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="749c0-172">**Microsoft.Compute/virtualMachines API version 2017-12-01 and earlier**</span></span>
   
   ```JSON
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2017-12-01",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[variables('vmName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "userAssigned",
                "identityIds": [
                   "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
                ]
            }
        },
        {
            "type": "Microsoft.Compute/virtualMachines/extensions",
            "name": "[concat(variables('vmName'),'/ManagedIdentityExtensionForLinux')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[resourceGroup().location]",
            "dependsOn": [
                "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
            ],
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
   ```

### <a name="remove-a-user-assigned-managed-identity-from-an-azure-vm"></a><span data-ttu-id="749c0-173">Remove a user-assigned managed identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="749c0-173">Remove a user-assigned managed identity from an Azure VM</span></span>

<span data-ttu-id="749c0-174">If you have a VM that no longer needs a user-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="749c0-174">If you have a VM that no longer needs a user-assigned managed identity:</span></span>

1. <span data-ttu-id="749c0-175">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="749c0-175">Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.</span></span>

2. <span data-ttu-id="749c0-176">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section.</span><span class="sxs-lookup"><span data-stu-id="749c0-176">Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section.</span></span> <span data-ttu-id="749c0-177">If you have a VM that only has user-assigned managed identity, you can disable it by changing the the identity type to `None`.</span><span class="sxs-lookup"><span data-stu-id="749c0-177">If you have a VM that only has user-assigned managed identity, you can disable it by changing the the identity type to `None`.</span></span>
 
   <span data-ttu-id="749c0-178">The following example shows you how remove all user-assigned managed identities from a VM with no system-assigned managed identities:</span><span class="sxs-lookup"><span data-stu-id="749c0-178">The following example shows you how remove all user-assigned managed identities from a VM with no system-assigned managed identities:</span></span>
   
   ```json
    {
      "apiVersion": "2018-06-01",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "identity": { 
          "type": "None"
    }
   ```
   
   <span data-ttu-id="749c0-179">**Microsoft.Compute/virtualMachines API version 2018-06-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="749c0-179">**Microsoft.Compute/virtualMachines API version 2018-06-01 and earlier**</span></span>
    
   <span data-ttu-id="749c0-180">To remove a single user-assigned managed identity from a VM, remove it from the `useraAssignedIdentities` dictionary.</span><span class="sxs-lookup"><span data-stu-id="749c0-180">To remove a single user-assigned managed identity from a VM, remove it from the `useraAssignedIdentities` dictionary.</span></span>

   <span data-ttu-id="749c0-181">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="749c0-181">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span></span>
 
   <span data-ttu-id="749c0-182">**Microsoft.Compute/virtualMachines API version 2017-12-01**</span><span class="sxs-lookup"><span data-stu-id="749c0-182">**Microsoft.Compute/virtualMachines API version 2017-12-01**</span></span>

   <span data-ttu-id="749c0-183">To remove a a single user-assigned managed identity from a VM, remove it from the `identityIds` array.</span><span class="sxs-lookup"><span data-stu-id="749c0-183">To remove a a single user-assigned managed identity from a VM, remove it from the `identityIds` array.</span></span>

   <span data-ttu-id="749c0-184">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="749c0-184">If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="749c0-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="749c0-185">Next steps</span></span>

- <span data-ttu-id="749c0-186">[Managed identities for Azure resources overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="749c0-186">[Managed identities for Azure resources overview](overview.md).</span></span>

