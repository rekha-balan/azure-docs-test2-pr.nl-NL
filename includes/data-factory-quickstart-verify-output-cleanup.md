## <a name="verify-the-output"></a><span data-ttu-id="68f5c-101">Verify the output</span><span class="sxs-lookup"><span data-stu-id="68f5c-101">Verify the output</span></span>
<span data-ttu-id="68f5c-102">The pipeline automatically creates the output folder in the adftutorial blob container.</span><span class="sxs-lookup"><span data-stu-id="68f5c-102">The pipeline automatically creates the output folder in the adftutorial blob container.</span></span> <span data-ttu-id="68f5c-103">Then, it copies the emp.txt file from the input folder to the output folder.</span><span class="sxs-lookup"><span data-stu-id="68f5c-103">Then, it copies the emp.txt file from the input folder to the output folder.</span></span> 

1. <span data-ttu-id="68f5c-104">In the Azure portal, on the **adftutorial** container page, click **Refresh** to see the output folder.</span><span class="sxs-lookup"><span data-stu-id="68f5c-104">In the Azure portal, on the **adftutorial** container page, click **Refresh** to see the output folder.</span></span> 
    
    ![Refresh](media/data-factory-quickstart-verify-output-cleanup/output-refresh.png)
2. <span data-ttu-id="68f5c-106">Click **output** in the folder list.</span><span class="sxs-lookup"><span data-stu-id="68f5c-106">Click **output** in the folder list.</span></span> 
2. <span data-ttu-id="68f5c-107">Confirm that the **emp.txt** is copied to the output folder.</span><span class="sxs-lookup"><span data-stu-id="68f5c-107">Confirm that the **emp.txt** is copied to the output folder.</span></span> 

    ![Refresh](media/data-factory-quickstart-verify-output-cleanup/output-file.png)

## <a name="clean-up-resources"></a><span data-ttu-id="68f5c-109">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="68f5c-109">Clean up resources</span></span>
<span data-ttu-id="68f5c-110">You can clean up the resources that you created in the Quickstart in two ways.</span><span class="sxs-lookup"><span data-stu-id="68f5c-110">You can clean up the resources that you created in the Quickstart in two ways.</span></span> <span data-ttu-id="68f5c-111">You can delete the [Azure resource group](../articles/azure-resource-manager/resource-group-overview.md), which includes all the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="68f5c-111">You can delete the [Azure resource group](../articles/azure-resource-manager/resource-group-overview.md), which includes all the resources in the resource group.</span></span> <span data-ttu-id="68f5c-112">If you want to keep the other resources intact, delete only the data factory you created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="68f5c-112">If you want to keep the other resources intact, delete only the data factory you created in this tutorial.</span></span>

<span data-ttu-id="68f5c-113">Deleting a resource group deletes all resources including data factories in it.</span><span class="sxs-lookup"><span data-stu-id="68f5c-113">Deleting a resource group deletes all resources including data factories in it.</span></span> <span data-ttu-id="68f5c-114">Run the following command to delete the entire resource group:</span><span class="sxs-lookup"><span data-stu-id="68f5c-114">Run the following command to delete the entire resource group:</span></span> 
```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="68f5c-115">If you want to delete just the data factory, not the entire resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="68f5c-115">If you want to delete just the data factory, not the entire resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```