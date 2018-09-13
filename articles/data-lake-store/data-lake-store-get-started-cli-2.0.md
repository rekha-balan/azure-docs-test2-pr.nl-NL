---
title: Use Azure command-line 2.0 interface to get started with Azure Data Lake Store | Microsoft Docs
description: Use Azure cross-platform command line 2.0 to create a Data Lake Store account and perform basic operations
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: nitinme
ms.openlocfilehash: c9d5fdc2ff27454b2492751034b43658ee9d46c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660686"
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20-preview"></a><span data-ttu-id="a3e77-103">Get started with Azure Data Lake Store using Azure CLI 2.0 (Preview)</span><span class="sxs-lookup"><span data-stu-id="a3e77-103">Get started with Azure Data Lake Store using Azure CLI 2.0 (Preview)</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a3e77-113">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3e77-113">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="a3e77-114">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a3e77-114">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="a3e77-115">It can be used on macOS, Linux, and Windows.</span><span class="sxs-lookup"><span data-stu-id="a3e77-115">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="a3e77-116">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3e77-116">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="a3e77-117">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span><span class="sxs-lookup"><span data-stu-id="a3e77-117">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a3e77-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3e77-118">Prerequisites</span></span>
<span data-ttu-id="a3e77-119">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="a3e77-119">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="a3e77-120">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="a3e77-120">**An Azure subscription**.</span></span> <span data-ttu-id="a3e77-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3e77-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a3e77-122">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span><span class="sxs-lookup"><span data-stu-id="a3e77-122">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="a3e77-123">Authentication</span><span class="sxs-lookup"><span data-stu-id="a3e77-123">Authentication</span></span>

<span data-ttu-id="a3e77-124">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span><span class="sxs-lookup"><span data-stu-id="a3e77-124">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="a3e77-125">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span><span class="sxs-lookup"><span data-stu-id="a3e77-125">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="a3e77-126">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="a3e77-126">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a3e77-127">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a3e77-127">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="enable-data-lake-store-preview-in-azure-cli-20"></a><span data-ttu-id="a3e77-128">Enable Data Lake Store (Preview) in Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a3e77-128">Enable Data Lake Store (Preview) in Azure CLI 2.0</span></span>

<span data-ttu-id="a3e77-129">Data Lake Store CLI 2.0 is currently in Preview and does not get enabled by default when you install Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a3e77-129">Data Lake Store CLI 2.0 is currently in Preview and does not get enabled by default when you install Azure CLI 2.0.</span></span> <span data-ttu-id="a3e77-130">Run the following command to enable Data Lake Store CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a3e77-130">Run the following command to enable Data Lake Store CLI 2.0.</span></span>

```azurecli
az component update --add dls
```


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="a3e77-131">Log in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a3e77-131">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="a3e77-132">Log into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a3e77-132">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="a3e77-133">You get a code to use in the next step.</span><span class="sxs-lookup"><span data-stu-id="a3e77-133">You get a code to use in the next step.</span></span> <span data-ttu-id="a3e77-134">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span><span class="sxs-lookup"><span data-stu-id="a3e77-134">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="a3e77-135">You are prompted to log in using your credentials.</span><span class="sxs-lookup"><span data-stu-id="a3e77-135">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="a3e77-136">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-136">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="a3e77-137">Use the following command to use a specific subscription.</span><span class="sxs-lookup"><span data-stu-id="a3e77-137">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="a3e77-138">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-138">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="a3e77-139">Create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="a3e77-139">Create a new resource group.</span></span> <span data-ttu-id="a3e77-140">In the following command, provide the parameter values you want to use.</span><span class="sxs-lookup"><span data-stu-id="a3e77-140">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="a3e77-141">If the location name contains spaces, put it in quotes.</span><span class="sxs-lookup"><span data-stu-id="a3e77-141">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="a3e77-142">For example "East US 2".</span><span class="sxs-lookup"><span data-stu-id="a3e77-142">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="a3e77-143">Create the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-143">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="a3e77-144">Create folders in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-144">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="a3e77-145">You can create folders under your Azure Data Lake Store account to manage and store data.</span><span class="sxs-lookup"><span data-stu-id="a3e77-145">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="a3e77-146">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a3e77-146">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> The `--folder` parameter ensures that the command creates a folder. If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="a3e77-149">Upload data to a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-149">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="a3e77-150">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-150">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="a3e77-151">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a3e77-151">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="a3e77-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="a3e77-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="a3e77-153">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="a3e77-153">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> For the destination, you must specify the complete path including the file name.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="a3e77-155">List files in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-155">List files in a Data Lake Store account</span></span>

<span data-ttu-id="a3e77-156">Use the following command to list the files in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-156">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="a3e77-157">The output of this should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="a3e77-157">The output of this should be similar to the following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="a3e77-158">Rename, download, and delete data from a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-158">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="a3e77-159">**To rename a file**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-159">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="a3e77-160">**To download a file**, use the following command.</span><span class="sxs-lookup"><span data-stu-id="a3e77-160">**To download a file**, use the following command.</span></span> <span data-ttu-id="a3e77-161">Make sure the destination path you specify already exists.</span><span class="sxs-lookup"><span data-stu-id="a3e77-161">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > The command creates the destination folder if it does not exist.
    > 
    >

* <span data-ttu-id="a3e77-163">**To delete a file**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-163">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="a3e77-164">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span><span class="sxs-lookup"><span data-stu-id="a3e77-164">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="a3e77-165">Work with permissions and ACLs for a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-165">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="a3e77-166">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a3e77-166">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="a3e77-167">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a3e77-167">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="a3e77-168">**To update the owner of a file/folder**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-168">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a3e77-169">**To update the permissions for a file/folder**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-169">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="a3e77-170">**To get the ACLs for a given path**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-170">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="a3e77-171">The output should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="a3e77-171">The output should be similar to the following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="a3e77-172">**To set an entry for an ACL**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-172">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="a3e77-173">**To remove an entry for an ACL**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-173">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a3e77-174">**To remove an entire default ACL**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-174">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="a3e77-175">**To remove an entire non-default ACL**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a3e77-175">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="a3e77-176">Delete a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="a3e77-176">Delete a Data Lake Store account</span></span>
<span data-ttu-id="a3e77-177">Use the following command to delete a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-177">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="a3e77-178">When prompted, enter **Y** to delete the account.</span><span class="sxs-lookup"><span data-stu-id="a3e77-178">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3e77-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3e77-179">Next steps</span></span>

* [<span data-ttu-id="a3e77-180">Azure Data Lake Store CLI 2.0 reference</span><span class="sxs-lookup"><span data-stu-id="a3e77-180">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="a3e77-181">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a3e77-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a3e77-182">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a3e77-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a3e77-183">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a3e77-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
