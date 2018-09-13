---
title: Sample data in Azure blob storage | Microsoft Docs
description: Sample data in Azure Blob Storage
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: ffb92df0e0727d02985ec26f61739cdc759d0f93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868289"
---
# <a name="heading"></a><span data-ttu-id="72724-103">Sample data in Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="72724-103">Sample data in Azure blob storage</span></span>
<span data-ttu-id="72724-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span><span class="sxs-lookup"><span data-stu-id="72724-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="72724-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="72724-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="72724-106">**Why sample your data?**</span><span class="sxs-lookup"><span data-stu-id="72724-106">**Why sample your data?**</span></span>
<span data-ttu-id="72724-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span><span class="sxs-lookup"><span data-stu-id="72724-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="72724-108">This facilitates data understanding, exploration, and feature engineering.</span><span class="sxs-lookup"><span data-stu-id="72724-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="72724-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="72724-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="72724-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="72724-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="72724-111">Download and down-sample data</span><span class="sxs-lookup"><span data-stu-id="72724-111">Download and down-sample data</span></span>
1. <span data-ttu-id="72724-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span><span class="sxs-lookup"><span data-stu-id="72724-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="72724-113">Read data into a Pandas data-frame from the file downloaded above.</span><span class="sxs-lookup"><span data-stu-id="72724-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="72724-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span><span class="sxs-lookup"><span data-stu-id="72724-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="72724-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span><span class="sxs-lookup"><span data-stu-id="72724-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <a name="heading"></a><span data-ttu-id="72724-116">Upload data and read it into Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="72724-116">Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="72724-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="72724-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="72724-118">Write the data frame to a local file</span><span class="sxs-lookup"><span data-stu-id="72724-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="72724-119">Upload the local file to an Azure blob using the following sample code:</span><span class="sxs-lookup"><span data-stu-id="72724-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="72724-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span><span class="sxs-lookup"><span data-stu-id="72724-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![reader blob](./media/sample-data-blob/reader_blob.png)

