## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="ee950-101">Overview of Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ee950-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="ee950-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span><span class="sxs-lookup"><span data-stu-id="ee950-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="ee950-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span><span class="sxs-lookup"><span data-stu-id="ee950-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="ee950-104">Resource Group Overview</span><span class="sxs-lookup"><span data-stu-id="ee950-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="ee950-105">Sample template snippet for VM extensions</span><span class="sxs-lookup"><span data-stu-id="ee950-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="ee950-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span><span class="sxs-lookup"><span data-stu-id="ee950-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="ee950-107">Here is the format for specifying the extension configuration.</span><span class="sxs-lookup"><span data-stu-id="ee950-107">Here is the format for specifying the extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="ee950-108">As you can see from the above, the extension template contains two main parts:</span><span class="sxs-lookup"><span data-stu-id="ee950-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="ee950-109">Extension name, publisher and version</span><span class="sxs-lookup"><span data-stu-id="ee950-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="ee950-110">Extension Configuration.</span><span class="sxs-lookup"><span data-stu-id="ee950-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="ee950-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span><span class="sxs-lookup"><span data-stu-id="ee950-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="ee950-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="ee950-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="ee950-113">These can be determined as following:</span><span class="sxs-lookup"><span data-stu-id="ee950-113">These can be determined as following:</span></span>  

