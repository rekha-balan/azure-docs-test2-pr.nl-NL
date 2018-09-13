---
title: Create features for Azure blob storage data using Panda | Microsoft Docs
description: How to create features for data that is stored in Azure blob container with the Panda Python package.
services: machine-learning,storage
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 21f88c770047905e2063255e76ad024f052f94e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552425"
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="8424c-103">Create features for Azure blob storage data using Panda</span><span class="sxs-lookup"><span data-stu-id="8424c-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="8424c-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span><span class="sxs-lookup"><span data-stu-id="8424c-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="8424c-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span><span class="sxs-lookup"><span data-stu-id="8424c-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="8424c-106">This **menu** links to topics that describe how to create features for data in various environments.</span><span class="sxs-lookup"><span data-stu-id="8424c-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="8424c-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="8424c-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8424c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8424c-108">Prerequisites</span></span>
<span data-ttu-id="8424c-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span><span class="sxs-lookup"><span data-stu-id="8424c-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="8424c-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8424c-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="8424c-111">Load the data into a Pandas data frame</span><span class="sxs-lookup"><span data-stu-id="8424c-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="8424c-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span><span class="sxs-lookup"><span data-stu-id="8424c-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="8424c-113">Here are the steps to follow for this procedure:</span><span class="sxs-lookup"><span data-stu-id="8424c-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="8424c-114">Download the data from Azure blob with the following sample Python code using blob service.</span><span class="sxs-lookup"><span data-stu-id="8424c-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="8424c-115">Replace the variable in the code below with your specific values:</span><span class="sxs-lookup"><span data-stu-id="8424c-115">Replace the variable in the code below with your specific values:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="8424c-116">Read the data into a Pandas data-frame from the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="8424c-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="8424c-117">Now you are ready to explore the data and generate features on this dataset.</span><span class="sxs-lookup"><span data-stu-id="8424c-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <a name="blob-featuregen"></a><span data-ttu-id="8424c-118">Feature Generation</span><span class="sxs-lookup"><span data-stu-id="8424c-118">Feature Generation</span></span>
<span data-ttu-id="8424c-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span><span class="sxs-lookup"><span data-stu-id="8424c-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <a name="blob-countfeature"></a><span data-ttu-id="8424c-120">Indicator value based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="8424c-120">Indicator value based Feature Generation</span></span>
<span data-ttu-id="8424c-121">Categorical features can be created as follows:</span><span class="sxs-lookup"><span data-stu-id="8424c-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="8424c-122">Inspect the distribution of the categorical column:</span><span class="sxs-lookup"><span data-stu-id="8424c-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="8424c-123">Generate indicator values for each of the column values</span><span class="sxs-lookup"><span data-stu-id="8424c-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="8424c-124">Join the indicator column with the original data frame</span><span class="sxs-lookup"><span data-stu-id="8424c-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="8424c-125">Remove the original variable itself:</span><span class="sxs-lookup"><span data-stu-id="8424c-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a><span data-ttu-id="8424c-126">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="8424c-126">Binning Feature Generation</span></span>
<span data-ttu-id="8424c-127">For generating binned features, we proceed as follows:</span><span class="sxs-lookup"><span data-stu-id="8424c-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="8424c-128">Add a sequence of columns to bin a numeric column</span><span class="sxs-lookup"><span data-stu-id="8424c-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="8424c-129">Convert binning to a sequence of boolean variables</span><span class="sxs-lookup"><span data-stu-id="8424c-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="8424c-130">Finally, Join the dummy variables back to the original data frame</span><span class="sxs-lookup"><span data-stu-id="8424c-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a><span data-ttu-id="8424c-131">Writing data back to Azure blob and consuming in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8424c-131">Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="8424c-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span><span class="sxs-lookup"><span data-stu-id="8424c-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="8424c-133">Write the data frame to local file</span><span class="sxs-lookup"><span data-stu-id="8424c-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="8424c-134">Upload the data to Azure blob as follows:</span><span class="sxs-lookup"><span data-stu-id="8424c-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="8424c-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span><span class="sxs-lookup"><span data-stu-id="8424c-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![reader blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-process-data-blob/reader_blob.png)


