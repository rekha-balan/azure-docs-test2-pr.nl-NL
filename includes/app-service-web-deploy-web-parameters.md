<span data-ttu-id="e8cf8-101">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-101">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="e8cf8-102">The template includes a section called Parameters that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-102">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="e8cf8-103">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-103">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="e8cf8-104">Do not define parameters for values that will always stay the same.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-104">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="e8cf8-105">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-105">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

<span data-ttu-id="e8cf8-106">When defining parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-106">When defining parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span></span> <span data-ttu-id="e8cf8-107">Use the **defaultValue** field to assign a value to the parameter, if no value is provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-107">Use the **defaultValue** field to assign a value to the parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="e8cf8-108">We will describe each parameter in the template.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-108">We will describe each parameter in the template.</span></span>

### <a name="sitename"></a><span data-ttu-id="e8cf8-109">siteName</span><span class="sxs-lookup"><span data-stu-id="e8cf8-109">siteName</span></span>
<span data-ttu-id="e8cf8-110">The name of the web app that you wish to create.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-110">The name of the web app that you wish to create.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="e8cf8-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="e8cf8-111">hostingPlanName</span></span>
<span data-ttu-id="e8cf8-112">The name of the App Service plan to use for hosting the web app.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-112">The name of the App Service plan to use for hosting the web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="e8cf8-113">sku</span><span class="sxs-lookup"><span data-stu-id="e8cf8-113">sku</span></span>
<span data-ttu-id="e8cf8-114">The pricing tier for the hosting plan.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-114">The pricing tier for the hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "The pricing tier for the hosting plan."
      }
    }

<span data-ttu-id="e8cf8-115">The template defines the values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-115">The template defines the values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="e8cf8-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="e8cf8-116">workerSize</span></span>
<span data-ttu-id="e8cf8-117">The instance size of the hosting plan (small, medium, or large).</span><span class="sxs-lookup"><span data-stu-id="e8cf8-117">The instance size of the hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="e8cf8-118">The template defines the values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-118">The template defines the values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="e8cf8-119">The values correspond to small, medium and large.</span><span class="sxs-lookup"><span data-stu-id="e8cf8-119">The values correspond to small, medium and large.</span></span>

