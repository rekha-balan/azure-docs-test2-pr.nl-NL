<span data-ttu-id="addbf-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span><span class="sxs-lookup"><span data-stu-id="addbf-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="addbf-102">Provide the tag name and value.</span><span class="sxs-lookup"><span data-stu-id="addbf-102">Provide the tag name and value.</span></span>

### <a name="apply-literal-value-to-tag-name"></a><span data-ttu-id="addbf-103">Apply literal value to tag name</span><span class="sxs-lookup"><span data-stu-id="addbf-103">Apply literal value to tag name</span></span>
<span data-ttu-id="addbf-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span><span class="sxs-lookup"><span data-stu-id="addbf-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-object-to-tag-element"></a><span data-ttu-id="addbf-105">Apply object to tag element</span><span class="sxs-lookup"><span data-stu-id="addbf-105">Apply object to tag element</span></span>
<span data-ttu-id="addbf-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span><span class="sxs-lookup"><span data-stu-id="addbf-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="addbf-107">Each property in the object becomes a separate tag for the resource.</span><span class="sxs-lookup"><span data-stu-id="addbf-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="addbf-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span><span class="sxs-lookup"><span data-stu-id="addbf-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-json-string-to-tag-name"></a><span data-ttu-id="addbf-109">Apply JSON string to tag name</span><span class="sxs-lookup"><span data-stu-id="addbf-109">Apply JSON string to tag name</span></span>

<span data-ttu-id="addbf-110">To store many values in a single tag, apply a JSON string that represents the values.</span><span class="sxs-lookup"><span data-stu-id="addbf-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="addbf-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span><span class="sxs-lookup"><span data-stu-id="addbf-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="addbf-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span><span class="sxs-lookup"><span data-stu-id="addbf-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```