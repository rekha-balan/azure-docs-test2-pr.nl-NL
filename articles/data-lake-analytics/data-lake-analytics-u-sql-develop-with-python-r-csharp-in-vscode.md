---
title: Develop U-SQL with Python, R, and C# for Azure Data Lake Analytics in Visual Studio Code
description: Learn how to use code behind with Python, R and C# to submit job in Azure Data Lake.
services: data-lake-analytics
ms.service: data-lake-analytics
author: jejiang
ms.author: jejiang
ms.reviewer: jasonwhowell
ms.topic: conceptual
ms.date: 11/22/2017
ms.openlocfilehash: 53859f5a81cf1d797ec93e83d75df5a329590dce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967201"
---
# <a name="develop-u-sql-with-python-r-and-c-for-azure-data-lake-analytics-in-visual-studio-code"></a><span data-ttu-id="822e7-103">Develop U-SQL with Python, R, and C# for Azure Data Lake Analytics in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="822e7-103">Develop U-SQL with Python, R, and C# for Azure Data Lake Analytics in Visual Studio Code</span></span>
<span data-ttu-id="822e7-104">Learn how to use Visual Studio Code (VSCode) to write Python, R and C# code behind with U-SQL and submit jobs to Azure Data Lake service.</span><span class="sxs-lookup"><span data-stu-id="822e7-104">Learn how to use Visual Studio Code (VSCode) to write Python, R and C# code behind with U-SQL and submit jobs to Azure Data Lake service.</span></span> <span data-ttu-id="822e7-105">For more information about Azure Data Lake Tools for VSCode, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="822e7-105">For more information about Azure Data Lake Tools for VSCode, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

<span data-ttu-id="822e7-106">Before writing code-behind custom code, you need to open a folder or a workspace in VSCode.</span><span class="sxs-lookup"><span data-stu-id="822e7-106">Before writing code-behind custom code, you need to open a folder or a workspace in VSCode.</span></span>


## <a name="prerequisites-for-python-and-r"></a><span data-ttu-id="822e7-107">Prerequisites for Python and R</span><span class="sxs-lookup"><span data-stu-id="822e7-107">Prerequisites for Python and R</span></span>
<span data-ttu-id="822e7-108">Register Python and, R extensions assemblies for your ADL account.</span><span class="sxs-lookup"><span data-stu-id="822e7-108">Register Python and, R extensions assemblies for your ADL account.</span></span> 
1. <span data-ttu-id="822e7-109">Open your account in portal.</span><span class="sxs-lookup"><span data-stu-id="822e7-109">Open your account in portal.</span></span>
   - <span data-ttu-id="822e7-110">Select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="822e7-110">Select **Overview**.</span></span> 
   - <span data-ttu-id="822e7-111">Click **Sample Script**.</span><span class="sxs-lookup"><span data-stu-id="822e7-111">Click **Sample Script**.</span></span>
2. <span data-ttu-id="822e7-112">Click **More**.</span><span class="sxs-lookup"><span data-stu-id="822e7-112">Click **More**.</span></span>
3. <span data-ttu-id="822e7-113">Select **Install U-SQL Extensions**.</span><span class="sxs-lookup"><span data-stu-id="822e7-113">Select **Install U-SQL Extensions**.</span></span> 
4. <span data-ttu-id="822e7-114">Confirmation message is displayed after the U-SQL extensions are installed.</span><span class="sxs-lookup"><span data-stu-id="822e7-114">Confirmation message is displayed after the U-SQL extensions are installed.</span></span> 

  ![Set up the environment for python and R](./media/data-lake-analytics-data-lake-tools-for-vscode/setup-the-enrionment-for-python-and-r.png)

  > [!Note]
  > <span data-ttu-id="822e7-116">For best experiences on Python and R language service, please install VSCode Python and R extension.</span><span class="sxs-lookup"><span data-stu-id="822e7-116">For best experiences on Python and R language service, please install VSCode Python and R extension.</span></span> 

## <a name="develop-python-file"></a><span data-ttu-id="822e7-117">Develop Python file</span><span class="sxs-lookup"><span data-stu-id="822e7-117">Develop Python file</span></span>
1. <span data-ttu-id="822e7-118">Click the **New File** in your workspace.</span><span class="sxs-lookup"><span data-stu-id="822e7-118">Click the **New File** in your workspace.</span></span>
2. <span data-ttu-id="822e7-119">Write your code in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="822e7-119">Write your code in U-SQL.</span></span> <span data-ttu-id="822e7-120">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-120">The following is a code sample.</span></span>
    ```U-SQL
    REFERENCE ASSEMBLY [ExtPython];
    @t  = 
        SELECT * FROM 
        (VALUES
            ("D1","T1","A1","@foo Hello World @bar"),
            ("D2","T2","A2","@baz Hello World @beer")
        ) AS 
            D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer("pythonSample.usql.py", pyVersion : "3.5.1");

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();
    ```
    
3. <span data-ttu-id="822e7-121">Right-click a script file, and then select **ADL: Generate Python Code Behind File**.</span><span class="sxs-lookup"><span data-stu-id="822e7-121">Right-click a script file, and then select **ADL: Generate Python Code Behind File**.</span></span> 
4. <span data-ttu-id="822e7-122">The **xxx.usql.py** file is generated in your working folder.</span><span class="sxs-lookup"><span data-stu-id="822e7-122">The **xxx.usql.py** file is generated in your working folder.</span></span> <span data-ttu-id="822e7-123">Write your code in Python file.</span><span class="sxs-lookup"><span data-stu-id="822e7-123">Write your code in Python file.</span></span> <span data-ttu-id="822e7-124">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-124">The following is a code sample.</span></span>

    ```Python
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ```
5. <span data-ttu-id="822e7-125">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span><span class="sxs-lookup"><span data-stu-id="822e7-125">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span></span>

## <a name="develop-r-file"></a><span data-ttu-id="822e7-126">Develop R file</span><span class="sxs-lookup"><span data-stu-id="822e7-126">Develop R file</span></span>
1. <span data-ttu-id="822e7-127">Click the **New File** in your workspace.</span><span class="sxs-lookup"><span data-stu-id="822e7-127">Click the **New File** in your workspace.</span></span>
2. <span data-ttu-id="822e7-128">Write your code in U-SQL file.</span><span class="sxs-lookup"><span data-stu-id="822e7-128">Write your code in U-SQL file.</span></span> <span data-ttu-id="822e7-129">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-129">The following is a code sample.</span></span>
    ```U-SQL
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT SepalLength double,
                SepalWidth double,
                PetalLength double,
                PetalWidth double,
                Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput =
        REDUCE @ExtendedData
        ON Par
        PRODUCE Par,
                fit double,
                lwr double,
                upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile : "RClusterRun.usql.R", rReturnType : "dataframe", stringsAsFactors : false);
    OUTPUT @RScriptOutput
    TO @OutputFilePredictions
    USING Outputters.Tsv();
    ```
3. <span data-ttu-id="822e7-130">Right-click in **USQL** file, and then select **ADL: Generate R Code Behind File**.</span><span class="sxs-lookup"><span data-stu-id="822e7-130">Right-click in **USQL** file, and then select **ADL: Generate R Code Behind File**.</span></span> 
4. <span data-ttu-id="822e7-131">The **xxx.usql.r** file is generated in your working folder.</span><span class="sxs-lookup"><span data-stu-id="822e7-131">The **xxx.usql.r** file is generated in your working folder.</span></span> <span data-ttu-id="822e7-132">Write your code in R file.</span><span class="sxs-lookup"><span data-stu-id="822e7-132">Write your code in R file.</span></span> <span data-ttu-id="822e7-133">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-133">The following is a code sample.</span></span>

    ```R
    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence"))
    ```
5. <span data-ttu-id="822e7-134">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span><span class="sxs-lookup"><span data-stu-id="822e7-134">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span></span>

## <a name="develop-c-file"></a><span data-ttu-id="822e7-135">Develop C# file</span><span class="sxs-lookup"><span data-stu-id="822e7-135">Develop C# file</span></span>
<span data-ttu-id="822e7-136">A code-behind file is a C# file associated with a single U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="822e7-136">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="822e7-137">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span><span class="sxs-lookup"><span data-stu-id="822e7-137">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="822e7-138">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span><span class="sxs-lookup"><span data-stu-id="822e7-138">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="822e7-139">The code-behind file is put in the same folder as its peering U-SQL script file.</span><span class="sxs-lookup"><span data-stu-id="822e7-139">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="822e7-140">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="822e7-140">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="822e7-141">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="822e7-141">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="822e7-142">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="822e7-142">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

1. <span data-ttu-id="822e7-143">Click the **New File** in your workspace.</span><span class="sxs-lookup"><span data-stu-id="822e7-143">Click the **New File** in your workspace.</span></span>
2. <span data-ttu-id="822e7-144">Write your code in U-SQL file.</span><span class="sxs-lookup"><span data-stu-id="822e7-144">Write your code in U-SQL file.</span></span> <span data-ttu-id="822e7-145">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-145">The following is a code sample.</span></span>
    ```U-SQL
    @a = 
        EXTRACT 
            Iid int,
        Starts DateTime,
        Region string,
        Query string,
        DwellTime int,
        Results string,
        ClickedUrls string 
        FROM @"/Samples/Data/SearchLog.tsv" 
        USING Extractors.Tsv();

    @d =
        SELECT DISTINCT Region 
        FROM @a;

    @d1 = 
        PROCESS @d
        PRODUCE 
            Region string,
        Mkt string
        USING new USQLApplication_codebehind.MyProcessor();

    OUTPUT @d1 
        TO @"/output/SearchLogtest.txt" 
        USING Outputters.Tsv();
    ```
3. <span data-ttu-id="822e7-146">Right-click in **USQL** file, and then select **ADL: Generate CS Code Behind File**.</span><span class="sxs-lookup"><span data-stu-id="822e7-146">Right-click in **USQL** file, and then select **ADL: Generate CS Code Behind File**.</span></span> 
4. <span data-ttu-id="822e7-147">The **xxx.usql.cs** file is generated in your working folder.</span><span class="sxs-lookup"><span data-stu-id="822e7-147">The **xxx.usql.cs** file is generated in your working folder.</span></span> <span data-ttu-id="822e7-148">Write your code in CS file.</span><span class="sxs-lookup"><span data-stu-id="822e7-148">Write your code in CS file.</span></span> <span data-ttu-id="822e7-149">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="822e7-149">The following is a code sample.</span></span>

    ```CS
    namespace USQLApplication_codebehind
    {
        [SqlUserDefinedProcessor]

        public class MyProcessor : IProcessor
        {
            public override IRow Process(IRow input, IUpdatableRow output)
            {
                output.Set(0, input.Get<string>(0));
                output.Set(1, input.Get<string>(0));
                return output.AsReadOnly();
            } 
        }
    }
    ```
5. <span data-ttu-id="822e7-150">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span><span class="sxs-lookup"><span data-stu-id="822e7-150">Right-click in **USQL** file, you can click **Compile Script** or **Submit Job** to running job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="822e7-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="822e7-151">Next steps</span></span>
* [<span data-ttu-id="822e7-152">Use the Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="822e7-152">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
* [<span data-ttu-id="822e7-153">U-SQL local run and local debug with Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="822e7-153">U-SQL local run and local debug with Visual Studio Code</span></span>](data-lake-tools-for-vscode-local-run-and-debug.md)
* [<span data-ttu-id="822e7-154">Get started with Data Lake Analytics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="822e7-154">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="822e7-155">Get started with Data Lake Analytics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="822e7-155">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="822e7-156">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span><span class="sxs-lookup"><span data-stu-id="822e7-156">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="822e7-157">Use Data Lake Analytics(U-SQL) catalog</span><span class="sxs-lookup"><span data-stu-id="822e7-157">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
