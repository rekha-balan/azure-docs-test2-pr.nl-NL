### <a name="app-service-plan"></a><span data-ttu-id="ef57e-101">App Service plan</span><span class="sxs-lookup"><span data-stu-id="ef57e-101">App Service plan</span></span>
<span data-ttu-id="ef57e-102">Creates the service plan for hosting the web app.</span><span class="sxs-lookup"><span data-stu-id="ef57e-102">Creates the service plan for hosting the web app.</span></span> <span data-ttu-id="ef57e-103">You provide the name of the plan through the **hostingPlanName** parameter.</span><span class="sxs-lookup"><span data-stu-id="ef57e-103">You provide the name of the plan through the **hostingPlanName** parameter.</span></span> <span data-ttu-id="ef57e-104">The location of the plan is the same location used for the resource group.</span><span class="sxs-lookup"><span data-stu-id="ef57e-104">The location of the plan is the same location used for the resource group.</span></span> <span data-ttu-id="ef57e-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span><span class="sxs-lookup"><span data-stu-id="ef57e-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

