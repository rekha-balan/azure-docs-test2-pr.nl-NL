---
title: Process Azure blob data with advanced analytics | Microsoft Docs
description: Process Data in Azure Blob storage.
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 3daf86f59a84f8c442581160142dcf806173b626
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966680"
---
# <a name="heading"></a><span data-ttu-id="d09bd-103">Process Azure blob data with advanced analytics</span><span class="sxs-lookup"><span data-stu-id="d09bd-103">Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="d09bd-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d09bd-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="d09bd-105">Load the data into a Pandas data frame</span><span class="sxs-lookup"><span data-stu-id="d09bd-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="d09bd-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span><span class="sxs-lookup"><span data-stu-id="d09bd-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="d09bd-107">Here are the steps to follow for this procedure:</span><span class="sxs-lookup"><span data-stu-id="d09bd-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="d09bd-108">Download the data from Azure blob with the following sample Python code using blob service.</span><span class="sxs-lookup"><span data-stu-id="d09bd-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="d09bd-109">Replace the variable in the code below with your specific values:</span><span class="sxs-lookup"><span data-stu-id="d09bd-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="d09bd-110">Read the data into a Pandas data-frame from the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="d09bd-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="d09bd-111">Now you are ready to explore the data and generate features on this dataset.</span><span class="sxs-lookup"><span data-stu-id="d09bd-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <a name="blob-dataexploration"></a><span data-ttu-id="d09bd-112">Data Exploration</span><span class="sxs-lookup"><span data-stu-id="d09bd-112">Data Exploration</span></span>
<span data-ttu-id="d09bd-113">Here are a few examples of ways to explore data using Pandas:</span><span class="sxs-lookup"><span data-stu-id="d09bd-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="d09bd-114">Inspect the number of rows and columns</span><span class="sxs-lookup"><span data-stu-id="d09bd-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="d09bd-115">Inspect the first or last few rows in the dataset as below:</span><span class="sxs-lookup"><span data-stu-id="d09bd-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="d09bd-116">Check the data type each column was imported as using the following sample code</span><span class="sxs-lookup"><span data-stu-id="d09bd-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="d09bd-117">Check the basic stats for the columns in the data set as follows</span><span class="sxs-lookup"><span data-stu-id="d09bd-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="d09bd-118">Look at the number of entries for each column value as follows</span><span class="sxs-lookup"><span data-stu-id="d09bd-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="d09bd-119">Count missing values versus the actual number of entries in each column using the following sample code</span><span class="sxs-lookup"><span data-stu-id="d09bd-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="d09bd-120">If you have missing values for a specific column in the data, you can drop them as follows:</span><span class="sxs-lookup"><span data-stu-id="d09bd-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="d09bd-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="d09bd-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="d09bd-122">Another way to replace missing values is with the mode function:</span><span class="sxs-lookup"><span data-stu-id="d09bd-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="d09bd-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="d09bd-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="d09bd-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span><span class="sxs-lookup"><span data-stu-id="d09bd-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="d09bd-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span><span class="sxs-lookup"><span data-stu-id="d09bd-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a><span data-ttu-id="d09bd-126">Feature Generation</span><span class="sxs-lookup"><span data-stu-id="d09bd-126">Feature Generation</span></span>
<span data-ttu-id="d09bd-127">We can generate features using Python as follows:</span><span class="sxs-lookup"><span data-stu-id="d09bd-127">We can generate features using Python as follows:</span></span>

### <a name="blob-countfeature"></a><span data-ttu-id="d09bd-128">Indicator value based Feature Generation</span><span class="sxs-lookup"><span data-stu-id="d09bd-128">Indicator value based Feature Generation</span></span>
<span data-ttu-id="d09bd-129">Categorical features can be created as follows:</span><span class="sxs-lookup"><span data-stu-id="d09bd-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="d09bd-130">Inspect the distribution of the categorical column:</span><span class="sxs-lookup"><span data-stu-id="d09bd-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="d09bd-131">Generate indicator values for each of the column values</span><span class="sxs-lookup"><span data-stu-id="d09bd-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="d09bd-132">Join the indicator column with the original data frame</span><span class="sxs-lookup"><span data-stu-id="d09bd-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="d09bd-133">Remove the original variable itself:</span><span class="sxs-lookup"><span data-stu-id="d09bd-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a><span data-ttu-id="d09bd-134">Binning Feature Generation</span><span class="sxs-lookup"><span data-stu-id="d09bd-134">Binning Feature Generation</span></span>
<span data-ttu-id="d09bd-135">For generating binned features, we proceed as follows:</span><span class="sxs-lookup"><span data-stu-id="d09bd-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="d09bd-136">Add a sequence of columns to bin a numeric column</span><span class="sxs-lookup"><span data-stu-id="d09bd-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="d09bd-137">Convert binning to a sequence of boolean variables</span><span class="sxs-lookup"><span data-stu-id="d09bd-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="d09bd-138">Finally, Join the dummy variables back to the original data frame</span><span class="sxs-lookup"><span data-stu-id="d09bd-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <a name="sql-featuregen"></a><span data-ttu-id="d09bd-139">Writing data back to Azure blob and consuming in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d09bd-139">Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="d09bd-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span><span class="sxs-lookup"><span data-stu-id="d09bd-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="d09bd-141">Write the data frame to local file</span><span class="sxs-lookup"><span data-stu-id="d09bd-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="d09bd-142">Upload the data to Azure blob as follows:</span><span class="sxs-lookup"><span data-stu-id="d09bd-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="d09bd-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span><span class="sxs-lookup"><span data-stu-id="d09bd-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![reader blob][1]

[1]: ./media/data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

