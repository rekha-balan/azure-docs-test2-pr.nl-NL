---
title: Create and publish an Azure service catalog managed application | Microsoft Docs
description: Shows how to create an Azure managed application that is intended for members of your organization.
services: managed-applications
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.date: 06/08/2018
ms.author: tomfitz
ms.openlocfilehash: 3b1da6e9068be3c96cce5973f29344fe7e4b4872
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866101"
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="e79bb-103">Publish a managed application for internal consumption</span><span class="sxs-lookup"><span data-stu-id="e79bb-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="e79bb-104">You can create and publish Azure [managed applications](overview.md) that are intended for members of your organization.</span><span class="sxs-lookup"><span data-stu-id="e79bb-104">You can create and publish Azure [managed applications](overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="e79bb-105">For example, an IT department can publish managed applications that fulfill organizational standards.</span><span class="sxs-lookup"><span data-stu-id="e79bb-105">For example, an IT department can publish managed applications that fulfill organizational standards.</span></span> <span data-ttu-id="e79bb-106">These managed applications are available through the service catalog, not the Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="e79bb-106">These managed applications are available through the service catalog, not the Azure marketplace.</span></span>

<span data-ttu-id="e79bb-107">To publish a managed application for the service catalog, you must:</span><span class="sxs-lookup"><span data-stu-id="e79bb-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="e79bb-108">Create a template that defines the resources to deploy with the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-108">Create a template that defines the resources to deploy with the managed application.</span></span>
* <span data-ttu-id="e79bb-109">Define the user interface elements for the portal when deploying the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-109">Define the user interface elements for the portal when deploying the managed application.</span></span>
* <span data-ttu-id="e79bb-110">Create a .zip package that contains the required template files.</span><span class="sxs-lookup"><span data-stu-id="e79bb-110">Create a .zip package that contains the required template files.</span></span>
* <span data-ttu-id="e79bb-111">Decide which user, group, or application needs access to the resource group in the user's subscription.</span><span class="sxs-lookup"><span data-stu-id="e79bb-111">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="e79bb-112">Create the managed application definition that points to the .zip package and requests access for the identity.</span><span class="sxs-lookup"><span data-stu-id="e79bb-112">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

<span data-ttu-id="e79bb-113">For this article, your managed application has only a storage account.</span><span class="sxs-lookup"><span data-stu-id="e79bb-113">For this article, your managed application has only a storage account.</span></span> <span data-ttu-id="e79bb-114">It's intended to illustrate the steps of publishing a managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-114">It's intended to illustrate the steps of publishing a managed application.</span></span> <span data-ttu-id="e79bb-115">For complete examples, see [Sample projects for Azure managed applications](sample-projects.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-115">For complete examples, see [Sample projects for Azure managed applications](sample-projects.md).</span></span>

<span data-ttu-id="e79bb-116">The PowerShell examples in this article require Azure PowerShell 6.2 or later.</span><span class="sxs-lookup"><span data-stu-id="e79bb-116">The PowerShell examples in this article require Azure PowerShell 6.2 or later.</span></span> <span data-ttu-id="e79bb-117">If needed, [update your version](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e79bb-117">If needed, [update your version](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-the-resource-template"></a><span data-ttu-id="e79bb-118">Create the resource template</span><span class="sxs-lookup"><span data-stu-id="e79bb-118">Create the resource template</span></span>

<span data-ttu-id="e79bb-119">Every managed application definition includes a file named **mainTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-119">Every managed application definition includes a file named **mainTemplate.json**.</span></span> <span data-ttu-id="e79bb-120">In it, you define the Azure resources to deploy.</span><span class="sxs-lookup"><span data-stu-id="e79bb-120">In it, you define the Azure resources to deploy.</span></span> <span data-ttu-id="e79bb-121">The template is no different than a regular Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="e79bb-121">The template is no different than a regular Resource Manager template.</span></span>

<span data-ttu-id="e79bb-122">Create a file named **mainTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-122">Create a file named **mainTemplate.json**.</span></span> <span data-ttu-id="e79bb-123">The name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e79bb-123">The name is case-sensitive.</span></span>

<span data-ttu-id="e79bb-124">Add the following JSON to your file.</span><span class="sxs-lookup"><span data-stu-id="e79bb-124">Add the following JSON to your file.</span></span> <span data-ttu-id="e79bb-125">It defines the parameters for creating a storage account, and specifies the properties for the storage account.</span><span class="sxs-lookup"><span data-stu-id="e79bb-125">It defines the parameters for creating a storage account, and specifies the properties for the storage account.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        },
        "storageAccountType": {
            "type": "string"
        },
        "location": {
            "type": "string",
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {
        "storageAccountName": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[variables('storageAccountName')]",
            "apiVersion": "2016-01-01",
            "location": "[parameters('location')]",
            "sku": {
                "name": "[parameters('storageAccountType')]"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {
        "storageEndpoint": {
            "type": "string",
            "value": "[reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
        }
    }
}
```

<span data-ttu-id="e79bb-126">Save the mainTemplate.json file.</span><span class="sxs-lookup"><span data-stu-id="e79bb-126">Save the mainTemplate.json file.</span></span>

## <a name="create-the-user-interface-definition"></a><span data-ttu-id="e79bb-127">Create the user interface definition</span><span class="sxs-lookup"><span data-stu-id="e79bb-127">Create the user interface definition</span></span>

<span data-ttu-id="e79bb-128">The Azure portal uses the **createUiDefinition.json** file to generate the user interface for users who create the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-128">The Azure portal uses the **createUiDefinition.json** file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="e79bb-129">You define how users provide input for each parameter.</span><span class="sxs-lookup"><span data-stu-id="e79bb-129">You define how users provide input for each parameter.</span></span> <span data-ttu-id="e79bb-130">You can use options like a drop-down list, text box, password box, and other input tools.</span><span class="sxs-lookup"><span data-stu-id="e79bb-130">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="e79bb-131">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-131">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>

<span data-ttu-id="e79bb-132">Create a file named **createUiDefinition.json**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-132">Create a file named **createUiDefinition.json**.</span></span> <span data-ttu-id="e79bb-133">The name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e79bb-133">The name is case-sensitive.</span></span>

<span data-ttu-id="e79bb-134">Add the following JSON to the file.</span><span class="sxs-lookup"><span data-stu-id="e79bb-134">Add the following JSON to the file.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {}
        ],
        "steps": [
            {
                "name": "storageConfig",
                "label": "Storage settings",
                "subLabel": {
                    "preValidation": "Configure the infrastructure settings",
                    "postValidation": "Done"
                },
                "bladeTitle": "Storage settings",
                "elements": [
                    {
                        "name": "storageAccounts",
                        "type": "Microsoft.Storage.MultiStorageAccountCombo",
                        "label": {
                            "prefix": "Storage account name prefix",
                            "type": "Storage account type"
                        },
                        "defaultValue": {
                            "type": "Standard_LRS"
                        },
                        "constraints": {
                            "allowedTypes": [
                                "Premium_LRS",
                                "Standard_LRS",
                                "Standard_GRS"
                            ]
                        }
                    }
                ]
            }
        ],
        "outputs": {
            "storageAccountNamePrefix": "[steps('storageConfig').storageAccounts.prefix]",
            "storageAccountType": "[steps('storageConfig').storageAccounts.type]",
            "location": "[location()]"
        }
    }
}
```

<span data-ttu-id="e79bb-135">Save the createUiDefinition.json file.</span><span class="sxs-lookup"><span data-stu-id="e79bb-135">Save the createUiDefinition.json file.</span></span>

## <a name="package-the-files"></a><span data-ttu-id="e79bb-136">Package the files</span><span class="sxs-lookup"><span data-stu-id="e79bb-136">Package the files</span></span>

<span data-ttu-id="e79bb-137">Add the two files to a .zip file named app.zip.</span><span class="sxs-lookup"><span data-stu-id="e79bb-137">Add the two files to a .zip file named app.zip.</span></span> <span data-ttu-id="e79bb-138">The two files must be at the root level of the .zip file.</span><span class="sxs-lookup"><span data-stu-id="e79bb-138">The two files must be at the root level of the .zip file.</span></span> <span data-ttu-id="e79bb-139">If you put them in a folder, you receive an error when creating the managed application definition that states the required files aren't present.</span><span class="sxs-lookup"><span data-stu-id="e79bb-139">If you put them in a folder, you receive an error when creating the managed application definition that states the required files aren't present.</span></span> 

<span data-ttu-id="e79bb-140">Upload the package to an accessible location from where it can be consumed.</span><span class="sxs-lookup"><span data-stu-id="e79bb-140">Upload the package to an accessible location from where it can be consumed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name storageGroup -Location eastus
$storageAccount = New-AzureRmStorageAccount -ResourceGroupName storageGroup `
  -Name "mystorageaccount" `
  -Location eastus `
  -SkuName Standard_LRS `
  -Kind Storage

$ctx = $storageAccount.Context

New-AzureStorageContainer -Name appcontainer -Context $ctx -Permission blob

Set-AzureStorageBlobContent -File "D:\myapplications\app.zip" `
  -Container appcontainer `
  -Blob "app.zip" `
  -Context $ctx 
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="e79bb-141">Create the managed application definition</span><span class="sxs-lookup"><span data-stu-id="e79bb-141">Create the managed application definition</span></span>

### <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="e79bb-142">Create an Azure Active Directory user group or application</span><span class="sxs-lookup"><span data-stu-id="e79bb-142">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="e79bb-143">The next step is to select a user group or application for managing the resources on behalf of the customer.</span><span class="sxs-lookup"><span data-stu-id="e79bb-143">The next step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="e79bb-144">This user group or application has permissions on the managed resource group according to the role that is assigned.</span><span class="sxs-lookup"><span data-stu-id="e79bb-144">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="e79bb-145">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span><span class="sxs-lookup"><span data-stu-id="e79bb-145">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="e79bb-146">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span><span class="sxs-lookup"><span data-stu-id="e79bb-146">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="e79bb-147">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-147">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="e79bb-148">You need the object ID of the user group to use for managing the resources.</span><span class="sxs-lookup"><span data-stu-id="e79bb-148">You need the object ID of the user group to use for managing the resources.</span></span> 

```powershell
$groupID=(Get-AzureRmADGroup -DisplayName mygroup).Id
```

### <a name="get-the-role-definition-id"></a><span data-ttu-id="e79bb-149">Get the role definition ID</span><span class="sxs-lookup"><span data-stu-id="e79bb-149">Get the role definition ID</span></span>

<span data-ttu-id="e79bb-150">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-150">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="e79bb-151">Typically, you use the Owner or Contributor or Reader role.</span><span class="sxs-lookup"><span data-stu-id="e79bb-151">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="e79bb-152">The following command shows how to get the role definition ID for the Owner role:</span><span class="sxs-lookup"><span data-stu-id="e79bb-152">The following command shows how to get the role definition ID for the Owner role:</span></span>

```powershell
$ownerID=(Get-AzureRmRoleDefinition -Name Owner).Id
```

### <a name="create-the-managed-application-definition"></a><span data-ttu-id="e79bb-153">Create the managed application definition</span><span class="sxs-lookup"><span data-stu-id="e79bb-153">Create the managed application definition</span></span>

<span data-ttu-id="e79bb-154">If you don't already have a resource group for storing your managed application definition, create one now:</span><span class="sxs-lookup"><span data-stu-id="e79bb-154">If you don't already have a resource group for storing your managed application definition, create one now:</span></span>

```powershell
New-AzureRmResourceGroup -Name appDefinitionGroup -Location westcentralus
```

<span data-ttu-id="e79bb-155">Now, create the managed application definition resource.</span><span class="sxs-lookup"><span data-stu-id="e79bb-155">Now, create the managed application definition resource.</span></span>

```powershell
$blob = Get-AzureStorageBlob -Container appcontainer -Blob app.zip -Context $ctx

New-AzureRmManagedApplicationDefinition `
  -Name "ManagedStorage" `
  -Location "westcentralus" `
  -ResourceGroupName appDefinitionGroup `
  -LockLevel ReadOnly `
  -DisplayName "Managed Storage Account" `
  -Description "Managed Azure Storage Account" `
  -Authorization "${groupID}:$ownerID" `
  -PackageFileUri $blob.ICloudBlob.StorageUri.PrimaryUri.AbsoluteUri
```

### <a name="make-sure-users-can-see-your-definition"></a><span data-ttu-id="e79bb-156">Make sure users can see your definition</span><span class="sxs-lookup"><span data-stu-id="e79bb-156">Make sure users can see your definition</span></span>

<span data-ttu-id="e79bb-157">You have access to the managed application definition, but you want to make sure other users in your organization can access it.</span><span class="sxs-lookup"><span data-stu-id="e79bb-157">You have access to the managed application definition, but you want to make sure other users in your organization can access it.</span></span> <span data-ttu-id="e79bb-158">Grant them at least the Reader role on the definition.</span><span class="sxs-lookup"><span data-stu-id="e79bb-158">Grant them at least the Reader role on the definition.</span></span> <span data-ttu-id="e79bb-159">They may have inherited this level of access from the subscription or resource group.</span><span class="sxs-lookup"><span data-stu-id="e79bb-159">They may have inherited this level of access from the subscription or resource group.</span></span> <span data-ttu-id="e79bb-160">To check who has access to the definition and add users or groups, see [Use Role-Based Access Control to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-160">To check who has access to the definition and add users or groups, see [Use Role-Based Access Control to manage access to your Azure subscription resources](../role-based-access-control/role-assignments-portal.md).</span></span>

## <a name="create-the-managed-application"></a><span data-ttu-id="e79bb-161">Create the managed application</span><span class="sxs-lookup"><span data-stu-id="e79bb-161">Create the managed application</span></span>

<span data-ttu-id="e79bb-162">You can deploy the managed application through the portal, PowerShell, or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e79bb-162">You can deploy the managed application through the portal, PowerShell, or Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="e79bb-163">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e79bb-163">PowerShell</span></span>

<span data-ttu-id="e79bb-164">First, let's use PowerShell to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-164">First, let's use PowerShell to deploy the managed application.</span></span>

```powershell
# Create resource group
New-AzureRmResourceGroup -Name applicationGroup -Location westcentralus

# Get ID of managed application definition
$appid=(Get-AzureRmManagedApplicationDefinition -ResourceGroupName appDefinitionGroup -Name ManagedStorage).ManagedApplicationDefinitionId

# Create the managed application
New-AzureRmManagedApplication `
  -Name storageApp `
  -Location westcentralus `
  -Kind ServiceCatalog `
  -ResourceGroupName applicationGroup `
  -ManagedApplicationDefinitionId $appid `
  -ManagedResourceGroupName "InfrastructureGroup" `
  -Parameter "{`"storageAccountNamePrefix`": {`"value`": `"demostorage`"}, `"storageAccountType`": {`"value`": `"Standard_LRS`"}}"
```

<span data-ttu-id="e79bb-165">Your managed application and managed infrastructure now exist in the subscription.</span><span class="sxs-lookup"><span data-stu-id="e79bb-165">Your managed application and managed infrastructure now exist in the subscription.</span></span>

### <a name="portal"></a><span data-ttu-id="e79bb-166">Portal</span><span class="sxs-lookup"><span data-stu-id="e79bb-166">Portal</span></span>

<span data-ttu-id="e79bb-167">Now, let's use the portal to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-167">Now, let's use the portal to deploy the managed application.</span></span> <span data-ttu-id="e79bb-168">You see the user interface you created in the package.</span><span class="sxs-lookup"><span data-stu-id="e79bb-168">You see the user interface you created in the package.</span></span>

1. <span data-ttu-id="e79bb-169">Go to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e79bb-169">Go to the Azure portal.</span></span> <span data-ttu-id="e79bb-170">Select **+ Create a resource** and search for **service catalog**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-170">Select **+ Create a resource** and search for **service catalog**.</span></span>

   ![Search service catalog](./media/publish-service-catalog-app/create-new.png)

1. <span data-ttu-id="e79bb-172">Select **Service Catalog Managed Application**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-172">Select **Service Catalog Managed Application**.</span></span>

   ![Select service catalog](./media/publish-service-catalog-app/select-service-catalog-managed-app.png)

1. <span data-ttu-id="e79bb-174">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-174">Select **Create**.</span></span>

   ![Select create](./media/publish-service-catalog-app/select-create.png)

1. <span data-ttu-id="e79bb-176">Find the managed application you want to create from the list of available solutions, and select it.</span><span class="sxs-lookup"><span data-stu-id="e79bb-176">Find the managed application you want to create from the list of available solutions, and select it.</span></span> <span data-ttu-id="e79bb-177">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-177">Select **Create**.</span></span>

   ![Find the managed application](./media/publish-service-catalog-app/find-application.png)

   <span data-ttu-id="e79bb-179">If you can't see the managed application definition through the portal, you may need to change your portal settings.</span><span class="sxs-lookup"><span data-stu-id="e79bb-179">If you can't see the managed application definition through the portal, you may need to change your portal settings.</span></span> <span data-ttu-id="e79bb-180">Select the **Directory and Subscription filter**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-180">Select the **Directory and Subscription filter**.</span></span>

   ![Select subscription filter](./media/publish-service-catalog-app/select-filter.png)

   <span data-ttu-id="e79bb-182">Check that the global subscription filter includes the subscription that contains the managed application definition.</span><span class="sxs-lookup"><span data-stu-id="e79bb-182">Check that the global subscription filter includes the subscription that contains the managed application definition.</span></span>

   ![Check subscription filter](./media/publish-service-catalog-app/check-global-filter.png)

   <span data-ttu-id="e79bb-184">After selecting the subscription, start over with creating the service catalog managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-184">After selecting the subscription, start over with creating the service catalog managed application.</span></span> <span data-ttu-id="e79bb-185">You should see it now.</span><span class="sxs-lookup"><span data-stu-id="e79bb-185">You should see it now.</span></span>

1. <span data-ttu-id="e79bb-186">Provide basic information that is required for the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-186">Provide basic information that is required for the managed application.</span></span> <span data-ttu-id="e79bb-187">Specify the subscription and a new resource group to contain the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-187">Specify the subscription and a new resource group to contain the managed application.</span></span> <span data-ttu-id="e79bb-188">Select **West Central US** for location.</span><span class="sxs-lookup"><span data-stu-id="e79bb-188">Select **West Central US** for location.</span></span> <span data-ttu-id="e79bb-189">When done, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-189">When done, select **OK**.</span></span>

   ![Provide managed application parameters](./media/publish-service-catalog-app/add-basics.png)

1. <span data-ttu-id="e79bb-191">Provide values that are specific to the resources in the managed application.</span><span class="sxs-lookup"><span data-stu-id="e79bb-191">Provide values that are specific to the resources in the managed application.</span></span> <span data-ttu-id="e79bb-192">When done, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e79bb-192">When done, select **OK**.</span></span>

   ![Provide resource parameters](./media/publish-service-catalog-app/add-storage-settings.png)

1. <span data-ttu-id="e79bb-194">The template validates the values you provided.</span><span class="sxs-lookup"><span data-stu-id="e79bb-194">The template validates the values you provided.</span></span> <span data-ttu-id="e79bb-195">If validation succeeds, select **OK** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="e79bb-195">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Validate managed application](./media/publish-service-catalog-app/view-summary.png)

<span data-ttu-id="e79bb-197">After the deployment finishes, the managed application exists in a resource group named applicationGroup.</span><span class="sxs-lookup"><span data-stu-id="e79bb-197">After the deployment finishes, the managed application exists in a resource group named applicationGroup.</span></span> <span data-ttu-id="e79bb-198">The storage account exists in a resource group named applicationGroup plus a hashed string value.</span><span class="sxs-lookup"><span data-stu-id="e79bb-198">The storage account exists in a resource group named applicationGroup plus a hashed string value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e79bb-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="e79bb-199">Next steps</span></span>

* <span data-ttu-id="e79bb-200">For an introduction to managed applications, see [Managed application overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-200">For an introduction to managed applications, see [Managed application overview](overview.md).</span></span>
* <span data-ttu-id="e79bb-201">For example projects, see [Sample projects for Azure managed applications](sample-projects.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-201">For example projects, see [Sample projects for Azure managed applications](sample-projects.md).</span></span>
* <span data-ttu-id="e79bb-202">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e79bb-202">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
