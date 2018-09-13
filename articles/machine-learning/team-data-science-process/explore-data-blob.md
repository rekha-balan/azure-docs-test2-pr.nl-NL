---
title: Explore data in Azure blob storage with Pandas | Microsoft Docs
description: How to explore data that is stored in Azure blob container using Pandas.
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: deguhath
ms.openlocfilehash: 61943da154483d8e815fa135fba30b136724b011
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867657"
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="3b809-103">Explore data in Azure blob storage with Pandas</span><span class="sxs-lookup"><span data-stu-id="3b809-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="3b809-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span><span class="sxs-lookup"><span data-stu-id="3b809-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="3b809-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span><span class="sxs-lookup"><span data-stu-id="3b809-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="3b809-106">This task is a step in the [Data Science Process](overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b809-106">This task is a step in the [Data Science Process](overview.md).</span></span>

[!INCLUDE [cap-explore-data-selector](../../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="3b809-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b809-107">Prerequisites</span></span>
<span data-ttu-id="3b809-108">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="3b809-108">This article assumes that you have:</span></span>

* <span data-ttu-id="3b809-109">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="3b809-109">Created an Azure storage account.</span></span> <span data-ttu-id="3b809-110">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span><span class="sxs-lookup"><span data-stu-id="3b809-110">If you need instructions, see [Create an Azure Storage account](../../storage/common/storage-quickstart-create-account.md)</span></span>
* <span data-ttu-id="3b809-111">Stored your data in an Azure blob storage account.</span><span class="sxs-lookup"><span data-stu-id="3b809-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="3b809-112">If you need instructions, see [Moving data to and from Azure Storage](../../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="3b809-112">If you need instructions, see [Moving data to and from Azure Storage](../../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="3b809-113">Load the data into a Pandas DataFrame</span><span class="sxs-lookup"><span data-stu-id="3b809-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="3b809-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="3b809-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="3b809-115">Here are the steps to follow for this procedure:</span><span class="sxs-lookup"><span data-stu-id="3b809-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="3b809-116">Download the data from Azure blob with the following Python code sample using blob service.</span><span class="sxs-lookup"><span data-stu-id="3b809-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="3b809-117">Replace the variable in the following code with your specific values:</span><span class="sxs-lookup"><span data-stu-id="3b809-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="3b809-118">Read the data into a Pandas data-frame from the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="3b809-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="3b809-119">Now you are ready to explore the data and generate features on this dataset.</span><span class="sxs-lookup"><span data-stu-id="3b809-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <a name="blob-dataexploration"></a><span data-ttu-id="3b809-120">Examples of data exploration using Pandas</span><span class="sxs-lookup"><span data-stu-id="3b809-120">Examples of data exploration using Pandas</span></span>
<span data-ttu-id="3b809-121">Here are a few examples of ways to explore data using Pandas:</span><span class="sxs-lookup"><span data-stu-id="3b809-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="3b809-122">Inspect the **number of rows and columns**</span><span class="sxs-lookup"><span data-stu-id="3b809-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="3b809-123">**Inspect** the first or last few **rows** in the following dataset:</span><span class="sxs-lookup"><span data-stu-id="3b809-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="3b809-124">Check the **data type** each column was imported as using the following sample code</span><span class="sxs-lookup"><span data-stu-id="3b809-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="3b809-125">Check the **basic stats** for the columns in the data set as follows</span><span class="sxs-lookup"><span data-stu-id="3b809-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="3b809-126">Look at the number of entries for each column value as follows</span><span class="sxs-lookup"><span data-stu-id="3b809-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="3b809-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span><span class="sxs-lookup"><span data-stu-id="3b809-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="3b809-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span><span class="sxs-lookup"><span data-stu-id="3b809-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="3b809-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="3b809-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="3b809-130">Another way to replace missing values is with the mode function:</span><span class="sxs-lookup"><span data-stu-id="3b809-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="3b809-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="3b809-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="3b809-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span><span class="sxs-lookup"><span data-stu-id="3b809-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="3b809-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span><span class="sxs-lookup"><span data-stu-id="3b809-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

