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
# <a name="configure-managed-identities-for-azure-resources-on-a-azure-virtual-machine-scale-using-a-template"></a>Configure managed identities for Azure resources on a Azure virtual machine scale using a template

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory. You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code. 

In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure virtual machine scale set, using Azure Resource Manager deployment template:
- Enable and disable the system-assigned managed identity on an Azure virtual machine scale set
- Add and remove a user-assigned managed identity on an Azure virtual machine scale set

## <a name="prerequisites"></a>Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md). **Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.
- To perform the management operations in this article, your account needs the following Azure role based access control assignments:

    > [!NOTE]
    > No additional Azure AD directory role assignments required.

    - [Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.
    - [Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.
    - [Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager templates

As with the Azure portal and scripting, [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) templates provide the ability to deploy new or modified resources defined by an Azure resource group. Several options are available for template editing and deployment, both local and portal-based, including:

   - Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).
   - Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).
   - Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.
   - Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.  

Regardless of the option you choose, template syntax is the same during initial deployment and redeployment. Enabling managed identities for Azure resources on a new or existing VM is done in the same manner. Also, by default, Azure Resource Manager does an [incremental update](../../azure-resource-manager/deployment-modes.md) to deployments.

## <a name="system-assigned-managed-identity"></a>System-assigned managed identity

In this section, you will enable and disable the system-assigned managed identity using an Azure Resource Manager template.

### <a name="enable-system-assigned-managed-identity-during-creation-the-creation-of-a-virtual-machines-scale-set-or-a-existing-virtual-machine-scale-set"></a>Enable system-assigned managed identity during creation the creation of a virtual machines scale set or a existing virtual machine scale set

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.
   
2. To enable the system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachinesScaleSets` resource of interest within the resources section and add the `identity` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property. Use the following syntax:

   ```JSON
   "identity": { 
       "type": "SystemAssigned"
   }
   ```

3. (Optional) Add the virtual machine scale set managed identities for Azure resources extension as an `extensionsProfile` element. This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity, to retrieve tokens as well.  Use the following syntax:

   >[!NOTE] 
   > The following example assumes a Windows virtual machine scale set extension (`ManagedIdentityExtensionForWindows`) is being deployed. You can also configure for Linux by using `ManagedIdentityExtensionForLinux` instead, for the `"name"` and `"type"` elements.
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

4. When you're done, the following sections should added to the resource section of your template  and should resemble the following:

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

### <a name="disable-a-system-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a>Disable a system-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs a system-assigned managed identity:

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.

2. Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section. If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.

   **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

   If your apiVersion is `2018-06-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the userAssignedIdentities dictionary values.

   **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01 and earlier**

   If your apiVersion is `2017-12-01` and your virtual machine scale set has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities. 
   
    

   The following example shows you how remove a system-assigned managed identity from a virtual machine scale set with no user-assigned managed identities:
   
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

## <a name="user-assigned-managed-identity"></a>User-assigned managed identity

In this section, you assign a user-assigned managed identity to a virtual machine scale set using Azure Resource Manager template.

> [!Note]
> To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).

### <a name="assign-a-user-assigned-managed-identity-to-a-virutal-machine-scale-set"></a>Assign a user-assigned managed identity to a virutal machine scale set

1. Under the `resources` element, add the following entry to assign a user-assigned managed identity to your virtual machine scale set.  Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.
   
   **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

   If your apiVersion is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.

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

   **Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**
    
   If your `apiVersion` is `2017-12-01` or earlier, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the variables section of your template.

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

2. (Optional) Add the following entry under the `extensionProfile` element to assign the managed identities for Azure resources extension to your VMSS. This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well. Use the following syntax:
   
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

3. When you are done, your template should look similar to the following:
   
   **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**   

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

   **Microsoft.Compute/virtualMachines API version 2017-12-01 eand earlier**

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
### <a name="remove-user-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a>Remove user-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs a user-assigned managed identity:

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.

2. Load the template into an [editor](#azure-resource-manager-templates) and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section. If you have a virtual machine scale set that only has user-assigned managed identity, you can disable it by changing the the identity type to `None`.

   The following example shows you how remove all user-assigned managed identities from a VM with no system-assigned managed identities:

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
   
   **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**
    
   To remove a a single user-assigned managed identity from a virtual machine scale set, remove it from the `userAssignedIdentities` dictionary.

   If you have a system-assigned identity, keep it in the in the `type` value under the `identity` value.

   **Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**

   To remove a single user-assigned managed identity from a virtual machine scale set, remove it from the `identityIds` array.

   If you have a system-assigned managed identity, keep it in the in the `type` value under the `identity` value.
   
## <a name="next-steps"></a>Next steps

- [Managed identities for Azure resources overview](overview.md).
