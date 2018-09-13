<span data-ttu-id="6bc0f-101">If you use a parameter file to pass parameter values during deployment, you need to create a JSON file with a format similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="6bc0f-101">If you use a parameter file to pass parameter values during deployment, you need to create a JSON file with a format similar to the following example:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

<span data-ttu-id="6bc0f-102">The size of the parameter file cannot be more than 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6bc0f-102">The size of the parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="6bc0f-103">If you need to provide a sensitive value for a parameter (such as a password), add that value to a key vault.</span><span class="sxs-lookup"><span data-stu-id="6bc0f-103">If you need to provide a sensitive value for a parameter (such as a password), add that value to a key vault.</span></span> <span data-ttu-id="6bc0f-104">Retrieve the key vault during deployment as shown in the previous example.</span><span class="sxs-lookup"><span data-stu-id="6bc0f-104">Retrieve the key vault during deployment as shown in the previous example.</span></span> <span data-ttu-id="6bc0f-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="6bc0f-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

