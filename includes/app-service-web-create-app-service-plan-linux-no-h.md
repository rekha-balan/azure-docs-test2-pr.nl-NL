<span data-ttu-id="2921e-101">In the Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az_appservice_plan_create) command.</span><span class="sxs-lookup"><span data-stu-id="2921e-101">In the Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az_appservice_plan_create) command.</span></span>

<!-- [!INCLUDE [app-service-plan](app-service-plan-linux.md)] -->

<span data-ttu-id="2921e-102">The following example creates an App Service plan named `myAppServicePlan` in the **Basic** pricing tier (`--sku B1`) and in a Linux container (`--is-linux`).</span><span class="sxs-lookup"><span data-stu-id="2921e-102">The following example creates an App Service plan named `myAppServicePlan` in the **Basic** pricing tier (`--sku B1`) and in a Linux container (`--is-linux`).</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1 --is-linux
```

<span data-ttu-id="2921e-103">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="2921e-103">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "linux",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```
