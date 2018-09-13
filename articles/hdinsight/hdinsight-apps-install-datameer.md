---
title: Install published application - Datameer - Azure HDInsight
description: Install and use the Datameer third-party Hadoop application.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: a428bb7bc9cc6a6a2e28989271ad1998700438cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855688"
---
# <a name="install-published-application---datameer"></a><span data-ttu-id="d6581-103">Install published application - Datameer</span><span class="sxs-lookup"><span data-stu-id="d6581-103">Install published application - Datameer</span></span>

<span data-ttu-id="d6581-104">This article describes how to install and run the [Datameer](https://www.datameer.com/) published Hadoop application on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6581-104">This article describes how to install and run the [Datameer](https://www.datameer.com/) published Hadoop application on Azure HDInsight.</span></span> <span data-ttu-id="d6581-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d6581-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span> <span data-ttu-id="d6581-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d6581-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

## <a name="about-datameer"></a><span data-ttu-id="d6581-107">About Datameer</span><span class="sxs-lookup"><span data-stu-id="d6581-107">About Datameer</span></span>

<span data-ttu-id="d6581-108">Datameer is a native application for the Hadoop platform, extending existing Azure HDInsight capabilities and providing quick integration, preparation, and analysis of structured and unstructured data.</span><span class="sxs-lookup"><span data-stu-id="d6581-108">Datameer is a native application for the Hadoop platform, extending existing Azure HDInsight capabilities and providing quick integration, preparation, and analysis of structured and unstructured data.</span></span> <span data-ttu-id="d6581-109">Datameer can access more than 70 sources and formats: structured, semi-structured, and unstructured.</span><span class="sxs-lookup"><span data-stu-id="d6581-109">Datameer can access more than 70 sources and formats: structured, semi-structured, and unstructured.</span></span> <span data-ttu-id="d6581-110">You can directly upload data, or use their unique data links to pull data on demand.</span><span class="sxs-lookup"><span data-stu-id="d6581-110">You can directly upload data, or use their unique data links to pull data on demand.</span></span> <span data-ttu-id="d6581-111">Datameer’s self-service functionality and familiar spreadsheet interface reduces the complexity of Big Data technology and accelerates time to insight.</span><span class="sxs-lookup"><span data-stu-id="d6581-111">Datameer’s self-service functionality and familiar spreadsheet interface reduces the complexity of Big Data technology and accelerates time to insight.</span></span> <span data-ttu-id="d6581-112">The spreadsheet interface provides a simple mechanism for entering declarative formulas that are then translated to optimized Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="d6581-112">The spreadsheet interface provides a simple mechanism for entering declarative formulas that are then translated to optimized Hadoop jobs.</span></span> <span data-ttu-id="d6581-113">With Datameer and your business intelligence (BI) and Excel skills, you can use Hadoop in the cloud quickly.</span><span class="sxs-lookup"><span data-stu-id="d6581-113">With Datameer and your business intelligence (BI) and Excel skills, you can use Hadoop in the cloud quickly.</span></span> <span data-ttu-id="d6581-114">For more information, see the [Datameer documentation](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft).</span><span class="sxs-lookup"><span data-stu-id="d6581-114">For more information, see the [Datameer documentation](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6581-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6581-115">Prerequisites</span></span>

<span data-ttu-id="d6581-116">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span><span class="sxs-lookup"><span data-stu-id="d6581-116">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span></span>

* <span data-ttu-id="d6581-117">Cluster tier: Standard</span><span class="sxs-lookup"><span data-stu-id="d6581-117">Cluster tier: Standard</span></span>
* <span data-ttu-id="d6581-118">Cluster type: Hadoop</span><span class="sxs-lookup"><span data-stu-id="d6581-118">Cluster type: Hadoop</span></span>
* <span data-ttu-id="d6581-119">Cluster version: 3.4</span><span class="sxs-lookup"><span data-stu-id="d6581-119">Cluster version: 3.4</span></span>

## <a name="install-the-datameer-published-application"></a><span data-ttu-id="d6581-120">Install the Datameer published application</span><span class="sxs-lookup"><span data-stu-id="d6581-120">Install the Datameer published application</span></span>

<span data-ttu-id="d6581-121">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d6581-121">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span>

## <a name="launch-datameer"></a><span data-ttu-id="d6581-122">Launch Datameer</span><span class="sxs-lookup"><span data-stu-id="d6581-122">Launch Datameer</span></span>

1. <span data-ttu-id="d6581-123">After installation, you can launch Datameer from your cluster in Azure portal by going to the **Settings** pane, then clicking **Applications** under the **General** category.</span><span class="sxs-lookup"><span data-stu-id="d6581-123">After installation, you can launch Datameer from your cluster in Azure portal by going to the **Settings** pane, then clicking **Applications** under the **General** category.</span></span> <span data-ttu-id="d6581-124">The Installed Apps pane lists the installed applications.</span><span class="sxs-lookup"><span data-stu-id="d6581-124">The Installed Apps pane lists the installed applications.</span></span>

    ![Installed Datameer app](./media/hdinsight-apps-install-datameer/datameer-app.png)

2. <span data-ttu-id="d6581-126">When you select Datameer, you see a link to the web page and the SSH endpoint path.</span><span class="sxs-lookup"><span data-stu-id="d6581-126">When you select Datameer, you see a link to the web page and the SSH endpoint path.</span></span> <span data-ttu-id="d6581-127">Select the WEBPAGE link.</span><span class="sxs-lookup"><span data-stu-id="d6581-127">Select the WEBPAGE link.</span></span>

3. <span data-ttu-id="d6581-128">On first launch, there are two license options: either a free 14-day trial, or activate an existing license.</span><span class="sxs-lookup"><span data-stu-id="d6581-128">On first launch, there are two license options: either a free 14-day trial, or activate an existing license.</span></span>

    ![License options](./media/hdinsight-apps-install-datameer/license.png)

4. <span data-ttu-id="d6581-130">After completing your selected license option, you'll be presented with a login form.</span><span class="sxs-lookup"><span data-stu-id="d6581-130">After completing your selected license option, you'll be presented with a login form.</span></span> <span data-ttu-id="d6581-131">Enter the default credentials displayed prior to the login form.</span><span class="sxs-lookup"><span data-stu-id="d6581-131">Enter the default credentials displayed prior to the login form.</span></span> <span data-ttu-id="d6581-132">After logging in, accept the software agreement to continue.</span><span class="sxs-lookup"><span data-stu-id="d6581-132">After logging in, accept the software agreement to continue.</span></span>

    ![Login](./media/hdinsight-apps-install-datameer/login.png)

<span data-ttu-id="d6581-134">The following steps show a "Hello World" demonstration.</span><span class="sxs-lookup"><span data-stu-id="d6581-134">The following steps show a "Hello World" demonstration.</span></span>

1. <span data-ttu-id="d6581-135">[Download the sample CSV](https://datameer.box.com/s/wzzw27za3agic4yjj8zrn6vfrph0ppnf).</span><span class="sxs-lookup"><span data-stu-id="d6581-135">[Download the sample CSV](https://datameer.box.com/s/wzzw27za3agic4yjj8zrn6vfrph0ppnf).</span></span>

2. <span data-ttu-id="d6581-136">Click the **+** sign on top of the Datameer dashboard, and click **File Upload**.</span><span class="sxs-lookup"><span data-stu-id="d6581-136">Click the **+** sign on top of the Datameer dashboard, and click **File Upload**.</span></span>

    ![File Upload](./media/hdinsight-apps-install-datameer/upload.png)

3. <span data-ttu-id="d6581-138">In the upload dialog, browse and select the **Hello World.csv** file you downloaded.</span><span class="sxs-lookup"><span data-stu-id="d6581-138">In the upload dialog, browse and select the **Hello World.csv** file you downloaded.</span></span> <span data-ttu-id="d6581-139">Make sure the **File Type** is set to CSV / TSV.</span><span class="sxs-lookup"><span data-stu-id="d6581-139">Make sure the **File Type** is set to CSV / TSV.</span></span> <span data-ttu-id="d6581-140">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6581-140">Select **Next**.</span></span> <span data-ttu-id="d6581-141">Keep clicking **Next** until you reach the end of the wizard.</span><span class="sxs-lookup"><span data-stu-id="d6581-141">Keep clicking **Next** until you reach the end of the wizard.</span></span>

    ![File Upload](./media/hdinsight-apps-install-datameer/upload-browse.png)

4. <span data-ttu-id="d6581-143">Name the file **Hello World** underneath a New Folder.</span><span class="sxs-lookup"><span data-stu-id="d6581-143">Name the file **Hello World** underneath a New Folder.</span></span> <span data-ttu-id="d6581-144">Rename the new folder as "Demo".</span><span class="sxs-lookup"><span data-stu-id="d6581-144">Rename the new folder as "Demo".</span></span> <span data-ttu-id="d6581-145">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d6581-145">Select **Save**.</span></span>

    ![Save](./media/hdinsight-apps-install-datameer/save.png)

5. <span data-ttu-id="d6581-147">Click the **+** sign once more and select **Workbook** to create a new Workbook for the data.</span><span class="sxs-lookup"><span data-stu-id="d6581-147">Click the **+** sign once more and select **Workbook** to create a new Workbook for the data.</span></span>

    ![Add workbook](./media/hdinsight-apps-install-datameer/add-workbook.png)

6. <span data-ttu-id="d6581-149">Expand the **Data** folder, **FileUploads**, then the **Demo** folder you created when saving the "Hello World" file.</span><span class="sxs-lookup"><span data-stu-id="d6581-149">Expand the **Data** folder, **FileUploads**, then the **Demo** folder you created when saving the "Hello World" file.</span></span> <span data-ttu-id="d6581-150">Select **Hello World** form the list of files, then click **Add Data**.</span><span class="sxs-lookup"><span data-stu-id="d6581-150">Select **Hello World** form the list of files, then click **Add Data**.</span></span>

    ![Save](./media/hdinsight-apps-install-datameer/select-file.png)

7. <span data-ttu-id="d6581-152">You see the data loaded in a spreadsheet interface.</span><span class="sxs-lookup"><span data-stu-id="d6581-152">You see the data loaded in a spreadsheet interface.</span></span> <span data-ttu-id="d6581-153">To select a subset of the data, select the **Filter** button in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d6581-153">To select a subset of the data, select the **Filter** button in the toolbar.</span></span>

    ![Filter button](./media/hdinsight-apps-install-datameer/filter-button.png)

8. <span data-ttu-id="d6581-155">In the Apply Filter dialog, select the **City** column, **equals** operator, and type **Chicago** in the filter text box.</span><span class="sxs-lookup"><span data-stu-id="d6581-155">In the Apply Filter dialog, select the **City** column, **equals** operator, and type **Chicago** in the filter text box.</span></span> <span data-ttu-id="d6581-156">Check the **Create filter in new sheet** checkbox, then select **Create Filter**.</span><span class="sxs-lookup"><span data-stu-id="d6581-156">Check the **Create filter in new sheet** checkbox, then select **Create Filter**.</span></span>

    ![Apply Filter](./media/hdinsight-apps-install-datameer/apply-filter.png)

9. <span data-ttu-id="d6581-158">Save the Workbook by clicking **File**, then **Save**.</span><span class="sxs-lookup"><span data-stu-id="d6581-158">Save the Workbook by clicking **File**, then **Save**.</span></span> <span data-ttu-id="d6581-159">Supply a name, such as "Hello World Workbook".</span><span class="sxs-lookup"><span data-stu-id="d6581-159">Supply a name, such as "Hello World Workbook".</span></span>

10. <span data-ttu-id="d6581-160">You are presented with options for how and when to run the Workbook.</span><span class="sxs-lookup"><span data-stu-id="d6581-160">You are presented with options for how and when to run the Workbook.</span></span> <span data-ttu-id="d6581-161">For now, leave all of the options at their default values, then check the **Start calculation process immediately after save**, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d6581-161">For now, leave all of the options at their default values, then check the **Start calculation process immediately after save**, and select **Save**.</span></span>

    ![Save Workbook](./media/hdinsight-apps-install-datameer/save-workbook.png)

11. <span data-ttu-id="d6581-163">Datameer provides powerful visualization tools.</span><span class="sxs-lookup"><span data-stu-id="d6581-163">Datameer provides powerful visualization tools.</span></span> <span data-ttu-id="d6581-164">To display the data, create an Infographic.</span><span class="sxs-lookup"><span data-stu-id="d6581-164">To display the data, create an Infographic.</span></span> <span data-ttu-id="d6581-165">Select the **+** sign on top of the dashboard, then select **Infographic**.</span><span class="sxs-lookup"><span data-stu-id="d6581-165">Select the **+** sign on top of the dashboard, then select **Infographic**.</span></span>

    ![Add Infographic](./media/hdinsight-apps-install-datameer/infographic-button.png)

12. <span data-ttu-id="d6581-167">Drag a Bar Chart widget from the list of widgets on the left, as shown in step 1 in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="d6581-167">Drag a Bar Chart widget from the list of widgets on the left, as shown in step 1 in the following diagram.</span></span> <span data-ttu-id="d6581-168">Next, navigate through the Data folder under the data browser on the right, expand your Workbook, then the worksheet you added with the filter (step 2).</span><span class="sxs-lookup"><span data-stu-id="d6581-168">Next, navigate through the Data folder under the data browser on the right, expand your Workbook, then the worksheet you added with the filter (step 2).</span></span> <span data-ttu-id="d6581-169">Drag the **Name** column over the top of the bar chart and drop into the **Label** target to set the Workbook's Name column as the chart's label field (step 3).</span><span class="sxs-lookup"><span data-stu-id="d6581-169">Drag the **Name** column over the top of the bar chart and drop into the **Label** target to set the Workbook's Name column as the chart's label field (step 3).</span></span>

    ![Infographic](./media/hdinsight-apps-install-datameer/infographic.png)

13. <span data-ttu-id="d6581-171">To set Age as the chart's Y axis, drag the **Age** column into the chart's **Data** field.</span><span class="sxs-lookup"><span data-stu-id="d6581-171">To set Age as the chart's Y axis, drag the **Age** column into the chart's **Data** field.</span></span>

    ![Infographic](./media/hdinsight-apps-install-datameer/infographic-age.png)

<span data-ttu-id="d6581-173">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="d6581-173">Congratulations!</span></span> <span data-ttu-id="d6581-174">You've created a visualization of your data without writing any code.</span><span class="sxs-lookup"><span data-stu-id="d6581-174">You've created a visualization of your data without writing any code.</span></span> <span data-ttu-id="d6581-175">You can now explore variations and additional visualizations.</span><span class="sxs-lookup"><span data-stu-id="d6581-175">You can now explore variations and additional visualizations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6581-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6581-176">Next steps</span></span>

* <span data-ttu-id="d6581-177">[Datameer documentation](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft).</span><span class="sxs-lookup"><span data-stu-id="d6581-177">[Datameer documentation](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft).</span></span>
* <span data-ttu-id="d6581-178">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6581-178">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="d6581-179">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d6581-179">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="d6581-180">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="d6581-180">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="d6581-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="d6581-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="d6581-182">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="d6581-182">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span></span>
