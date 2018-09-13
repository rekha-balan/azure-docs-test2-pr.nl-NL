
<span data-ttu-id="7bd19-101">Create an app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span><span class="sxs-lookup"><span data-stu-id="7bd19-101">Create an app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span></span> 

<span data-ttu-id="7bd19-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span><span class="sxs-lookup"><span data-stu-id="7bd19-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="7bd19-103">In the following command, replace *\<app_name>* with a unique name.</span><span class="sxs-lookup"><span data-stu-id="7bd19-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="7bd19-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span><span class="sxs-lookup"><span data-stu-id="7bd19-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="7bd19-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="7bd19-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="7bd19-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd19-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```