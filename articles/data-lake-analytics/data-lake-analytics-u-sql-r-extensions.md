---
title: Extend U-SQL scripts with R in Azure Data Lake Analytics
description: Learn how to run R code in U-SQL scripts using Azure Data Lake Analytics
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.topic: conceptual
ms.date: 06/20/2017
ms.openlocfilehash: b7e6c4911081d3b83ed99ab7316cb6fd810a0d60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866497"
---
# <a name="extend-u-sql-scripts-with-r-code-in-azure-data-lake-analytics"></a><span data-ttu-id="c89e8-103">Extend U-SQL scripts with R code in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c89e8-103">Extend U-SQL scripts with R code in Azure Data Lake Analytics</span></span>

<span data-ttu-id="c89e8-104">The following example illustrates the basic steps for deploying R code:</span><span class="sxs-lookup"><span data-stu-id="c89e8-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="c89e8-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span><span class="sxs-lookup"><span data-stu-id="c89e8-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="c89e8-106">Use the` REDUCE` operation to partition the input data on a key.</span><span class="sxs-lookup"><span data-stu-id="c89e8-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="c89e8-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span><span class="sxs-lookup"><span data-stu-id="c89e8-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="c89e8-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span><span class="sxs-lookup"><span data-stu-id="c89e8-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="c89e8-109">Embedding R code in the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="c89e8-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="c89e8-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="c89e8-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="c89e8-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span><span class="sxs-lookup"><span data-stu-id="c89e8-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="c89e8-112">Keep the R code in a separate file and reference it  the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="c89e8-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="c89e8-113">The following example illustrates a more complex usage.</span><span class="sxs-lookup"><span data-stu-id="c89e8-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="c89e8-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="c89e8-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="c89e8-115">Save this R code as a separate file.</span><span class="sxs-lookup"><span data-stu-id="c89e8-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="c89e8-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span><span class="sxs-lookup"><span data-stu-id="c89e8-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="c89e8-117">How R Integrates with U-SQL</span><span class="sxs-lookup"><span data-stu-id="c89e8-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="c89e8-118">Datatypes</span><span class="sxs-lookup"><span data-stu-id="c89e8-118">Datatypes</span></span>
* <span data-ttu-id="c89e8-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="c89e8-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="c89e8-120">The `Factor` datatype is not supported in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c89e8-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="c89e8-121">`byte[]` must be serialized as a base64-encoded `string`.</span><span class="sxs-lookup"><span data-stu-id="c89e8-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="c89e8-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="c89e8-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="c89e8-123">Schemas</span><span class="sxs-lookup"><span data-stu-id="c89e8-123">Schemas</span></span>
* <span data-ttu-id="c89e8-124">U-SQL datasets cannot have duplicate column names.</span><span class="sxs-lookup"><span data-stu-id="c89e8-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="c89e8-125">U-SQL datasets column names must be strings.</span><span class="sxs-lookup"><span data-stu-id="c89e8-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="c89e8-126">Column names must be the same in U-SQL and R scripts.</span><span class="sxs-lookup"><span data-stu-id="c89e8-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="c89e8-127">Readonly column cannot be part of the output dataframe.</span><span class="sxs-lookup"><span data-stu-id="c89e8-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="c89e8-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span><span class="sxs-lookup"><span data-stu-id="c89e8-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="c89e8-129">Functional limitations</span><span class="sxs-lookup"><span data-stu-id="c89e8-129">Functional limitations</span></span>
* <span data-ttu-id="c89e8-130">The R Engine can't be instantiated twice in the same process.</span><span class="sxs-lookup"><span data-stu-id="c89e8-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="c89e8-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span><span class="sxs-lookup"><span data-stu-id="c89e8-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="c89e8-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="c89e8-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="c89e8-133">R Versions</span><span class="sxs-lookup"><span data-stu-id="c89e8-133">R Versions</span></span>
<span data-ttu-id="c89e8-134">Only R 3.2.2 is supported.</span><span class="sxs-lookup"><span data-stu-id="c89e8-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="c89e8-135">Standard R modules</span><span class="sxs-lookup"><span data-stu-id="c89e8-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="c89e8-136">Input and Output size limitations</span><span class="sxs-lookup"><span data-stu-id="c89e8-136">Input and Output size limitations</span></span>
<span data-ttu-id="c89e8-137">Every vertex has a limited amount of memory assigned to it.</span><span class="sxs-lookup"><span data-stu-id="c89e8-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="c89e8-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span><span class="sxs-lookup"><span data-stu-id="c89e8-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="c89e8-139">Sample Code</span><span class="sxs-lookup"><span data-stu-id="c89e8-139">Sample Code</span></span>
<span data-ttu-id="c89e8-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span><span class="sxs-lookup"><span data-stu-id="c89e8-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="c89e8-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="c89e8-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="c89e8-142">Deploying Custom R modules with U-SQL</span><span class="sxs-lookup"><span data-stu-id="c89e8-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="c89e8-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span><span class="sxs-lookup"><span data-stu-id="c89e8-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="c89e8-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span><span class="sxs-lookup"><span data-stu-id="c89e8-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="c89e8-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span><span class="sxs-lookup"><span data-stu-id="c89e8-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="c89e8-146">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c89e8-146">Next Steps</span></span>
* [<span data-ttu-id="c89e8-147">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c89e8-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c89e8-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c89e8-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c89e8-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="c89e8-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
