---
title: Integrate the Remote Monitoring solution with Azure Data Lake Store | Microsoft Docs
description: Learn how to integrate the Remote Monitoring solution with Azure Data Lake Store using an Azure Stream Analytics job.
author: philmea
manager: timlt
ms.author: philmea
ms.date: 04/29/2018
ms.topic: conceptual
ms.service: iot-accelerators
services: iot-accelerators
ms.openlocfilehash: a918866ff5e206ea4d2dedde2711424924a478fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864637"
---
# <a name="integrate-the-remote-monitoring-solution-with-azure-data-lake-store"></a><span data-ttu-id="851f1-103">Integrate the Remote Monitoring solution with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="851f1-103">Integrate the Remote Monitoring solution with Azure Data Lake Store</span></span>

<span data-ttu-id="851f1-104">You may have advanced analytics requirements beyond what is offered in the Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="851f1-104">You may have advanced analytics requirements beyond what is offered in the Remote Monitoring solution.</span></span> <span data-ttu-id="851f1-105">Azure Data Lake Store is ideal for this application because it can store data from massive and diverse datasets as well as integrate with Azure Data Lake Analytics to provide on-demand analytics.</span><span class="sxs-lookup"><span data-stu-id="851f1-105">Azure Data Lake Store is ideal for this application because it can store data from massive and diverse datasets as well as integrate with Azure Data Lake Analytics to provide on-demand analytics.</span></span>

<span data-ttu-id="851f1-106">In this how-to, you will use an Azure Stream Analytics job to stream data from the IoT hub in your Remote Monitoring solution to an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-106">In this how-to, you will use an Azure Stream Analytics job to stream data from the IoT hub in your Remote Monitoring solution to an Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="851f1-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="851f1-107">Prerequisites</span></span>

<span data-ttu-id="851f1-108">To complete this how-to, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="851f1-108">To complete this how-to, you will need the following:</span></span>

* <span data-ttu-id="851f1-109">[Deploy the Remote Monitoring solution accelerator](quickstart-remote-monitoring-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="851f1-109">[Deploy the Remote Monitoring solution accelerator](quickstart-remote-monitoring-deploy.md).</span></span>
  * <span data-ttu-id="851f1-110">The Remote Monitoring solution will deploy the IoT hub and Azure Stream Analytics job used in this article into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="851f1-110">The Remote Monitoring solution will deploy the IoT hub and Azure Stream Analytics job used in this article into your Azure subscription.</span></span>
* [<span data-ttu-id="851f1-111">Deploy an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="851f1-111">Deploy an Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
  * <span data-ttu-id="851f1-112">Your Data Lake Store should be deployed to the same region as your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="851f1-112">Your Data Lake Store should be deployed to the same region as your Remote Monitoring solution.</span></span>
  * <span data-ttu-id="851f1-113">[Create a folder](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) named "streaming" in your account.</span><span class="sxs-lookup"><span data-stu-id="851f1-113">[Create a folder](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) named "streaming" in your account.</span></span>

## <a name="create-a-consumer-group"></a><span data-ttu-id="851f1-114">Create a consumer group</span><span class="sxs-lookup"><span data-stu-id="851f1-114">Create a consumer group</span></span>

<span data-ttu-id="851f1-115">Create a dedicated consumer group in the IoT hub of your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="851f1-115">Create a dedicated consumer group in the IoT hub of your Remote Monitoring solution.</span></span> <span data-ttu-id="851f1-116">This will be used by the Stream Analytics job for streaming data to your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-116">This will be used by the Stream Analytics job for streaming data to your Data Lake Store.</span></span>

> [!NOTE]
> <span data-ttu-id="851f1-117">Consumer groups are used by applications to pull data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="851f1-117">Consumer groups are used by applications to pull data from Azure IoT Hub.</span></span> <span data-ttu-id="851f1-118">You should create a new consumer group for every five output consumers.</span><span class="sxs-lookup"><span data-stu-id="851f1-118">You should create a new consumer group for every five output consumers.</span></span> <span data-ttu-id="851f1-119">You can create up to 32 consumer groups.</span><span class="sxs-lookup"><span data-stu-id="851f1-119">You can create up to 32 consumer groups.</span></span>

1. <span data-ttu-id="851f1-120">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="851f1-120">Sign in to the Azure portal.</span></span>

1. <span data-ttu-id="851f1-121">In the Azure portal, click the **Cloud Shell** button.</span><span class="sxs-lookup"><span data-stu-id="851f1-121">In the Azure portal, click the **Cloud Shell** button.</span></span>

    ![Portal Launch Icon](./media/iot-accelerators-integrate-data-lake/portal-launch-icon.png)

1. <span data-ttu-id="851f1-123">Execute this command to create a new consumer group:</span><span class="sxs-lookup"><span data-stu-id="851f1-123">Execute this command to create a new consumer group:</span></span>

```azurecli-interactive
az iot hub consumer-group create --hub-name contoso-rm30263 --name streamanalyticsjob --resource-group contoso-rm
```

> [!NOTE]
> <span data-ttu-id="851f1-124">Use the resource group and IoT hub names from your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="851f1-124">Use the resource group and IoT hub names from your Remote Monitoring solution.</span></span>

## <a name="create-stream-analytics-job"></a><span data-ttu-id="851f1-125">Create Stream Analytics Job</span><span class="sxs-lookup"><span data-stu-id="851f1-125">Create Stream Analytics Job</span></span>

<span data-ttu-id="851f1-126">Create an Azure Stream Analytics job to stream the data from your IoT hub to your Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="851f1-126">Create an Azure Stream Analytics job to stream the data from your IoT hub to your Azure Data Lake store.</span></span>

1. <span data-ttu-id="851f1-127">Click **Create a resource**, select Internet of Things from the Marketplace, and click **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="851f1-127">Click **Create a resource**, select Internet of Things from the Marketplace, and click **Stream Analytics job**.</span></span>

    ![New Stream Analytics Job](./media/iot-accelerators-integrate-data-lake/new-stream-analytics-job.png)

1. <span data-ttu-id="851f1-129">Enter a job name and select the appropriate Subscription and Resource group.</span><span class="sxs-lookup"><span data-stu-id="851f1-129">Enter a job name and select the appropriate Subscription and Resource group.</span></span>

1. <span data-ttu-id="851f1-130">Select a Location in the near or in the same region as your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-130">Select a Location in the near or in the same region as your Data Lake Store.</span></span> <span data-ttu-id="851f1-131">Here we are using East US.</span><span class="sxs-lookup"><span data-stu-id="851f1-131">Here we are using East US.</span></span>

1. <span data-ttu-id="851f1-132">Ensure to leave the Hosting environment as the default **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="851f1-132">Ensure to leave the Hosting environment as the default **Cloud**.</span></span>

1. <span data-ttu-id="851f1-133">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="851f1-133">Click **Create**.</span></span>

    ![Create Stream Analytics Job](./media/iot-accelerators-integrate-data-lake/create-stream-analytics-job.png)

## <a name="configure-the-stream-analytics-job"></a><span data-ttu-id="851f1-135">Configure the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="851f1-135">Configure the Stream Analytics job</span></span>

1. <span data-ttu-id="851f1-136">Go to the **Stream Analytics job** in your Remote Monitoring solution resource group.</span><span class="sxs-lookup"><span data-stu-id="851f1-136">Go to the **Stream Analytics job** in your Remote Monitoring solution resource group.</span></span>

1. <span data-ttu-id="851f1-137">On the Overview page, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="851f1-137">On the Overview page, click **Inputs**.</span></span>

    ![Overview Page](./media/iot-accelerators-integrate-data-lake/stream-analytics-overview.png)

1. <span data-ttu-id="851f1-139">Click **Add stream input** and select **IoT Hub** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="851f1-139">Click **Add stream input** and select **IoT Hub** from the drop-down.</span></span>

    ![Add Input](./media/iot-accelerators-integrate-data-lake/stream-analytics-add-input.png)

1. <span data-ttu-id="851f1-141">On the New input tab, enter an Input alias of **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="851f1-141">On the New input tab, enter an Input alias of **IoTHub**.</span></span>

1. <span data-ttu-id="851f1-142">From the Consumer group drop-down, select the consumer group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="851f1-142">From the Consumer group drop-down, select the consumer group you created earlier.</span></span> <span data-ttu-id="851f1-143">Here we are using **streamanalyticsjob**.</span><span class="sxs-lookup"><span data-stu-id="851f1-143">Here we are using **streamanalyticsjob**.</span></span>

    ![Select Input](./media/iot-accelerators-integrate-data-lake/stream-analytics-new-input.png)

1. <span data-ttu-id="851f1-145">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="851f1-145">Click **Save**.</span></span>

1. <span data-ttu-id="851f1-146">On the Overview page, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="851f1-146">On the Overview page, click **Outputs**.</span></span>

    ![Add Data Lake Store](./media/iot-accelerators-integrate-data-lake/stream-analytics-overview-2.png)

1. <span data-ttu-id="851f1-148">Click **Add** and select **Data Lake Store** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="851f1-148">Click **Add** and select **Data Lake Store** from the drop-down.</span></span>

    ![Add Output](./media/iot-accelerators-integrate-data-lake/stream-analytics-output.png)

1. <span data-ttu-id="851f1-150">On the New output tab, enter an Output alias of **DataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="851f1-150">On the New output tab, enter an Output alias of **DataLakeStore**.</span></span>

1. <span data-ttu-id="851f1-151">Select the Data Lake Store account you created in previous steps and provide folder structure to stream data to the store.</span><span class="sxs-lookup"><span data-stu-id="851f1-151">Select the Data Lake Store account you created in previous steps and provide folder structure to stream data to the store.</span></span>

1. <span data-ttu-id="851f1-152">In the Date format field, enter **/streaming/{date}/{time}**.</span><span class="sxs-lookup"><span data-stu-id="851f1-152">In the Date format field, enter **/streaming/{date}/{time}**.</span></span> <span data-ttu-id="851f1-153">Leave the default Date format of YYYY/MM/DD and Time format of HH.</span><span class="sxs-lookup"><span data-stu-id="851f1-153">Leave the default Date format of YYYY/MM/DD and Time format of HH.</span></span>

    ![Provide Folder Structure](./media/iot-accelerators-integrate-data-lake/stream-analytics-new-output.png)

1. <span data-ttu-id="851f1-155">Click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="851f1-155">Click **Authorize**.</span></span>

    <span data-ttu-id="851f1-156">You will have to authorize with Data Lake Store to give the Stream analytics job write access to the file system.</span><span class="sxs-lookup"><span data-stu-id="851f1-156">You will have to authorize with Data Lake Store to give the Stream analytics job write access to the file system.</span></span>

    ![Authorize Stream Analytics to Data Lake Store](./media/iot-accelerators-integrate-data-lake/stream-analytics-out-authorize.png)

    <span data-ttu-id="851f1-158">You will see a popup and once the popup closes Authorize button will be greyed out after authorization is complete.</span><span class="sxs-lookup"><span data-stu-id="851f1-158">You will see a popup and once the popup closes Authorize button will be greyed out after authorization is complete.</span></span>

    > [!NOTE]
    > <span data-ttu-id="851f1-159">If you see an error in the popup window, open a new browser window in Incognito Mode and try again.</span><span class="sxs-lookup"><span data-stu-id="851f1-159">If you see an error in the popup window, open a new browser window in Incognito Mode and try again.</span></span>

1. <span data-ttu-id="851f1-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="851f1-160">Click **Save**.</span></span>

## <a name="edit-the-stream-analytics-query"></a><span data-ttu-id="851f1-161">Edit the Stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="851f1-161">Edit the Stream Analytics query</span></span>

<span data-ttu-id="851f1-162">Azure Stream Analytics uses a SQL-like query language to specify an input source that streams data, transform that data as desired, and output to a variety of storage or processing destinations.</span><span class="sxs-lookup"><span data-stu-id="851f1-162">Azure Stream Analytics uses a SQL-like query language to specify an input source that streams data, transform that data as desired, and output to a variety of storage or processing destinations.</span></span>

1. <span data-ttu-id="851f1-163">On the Overview tab, click **Edit query**.</span><span class="sxs-lookup"><span data-stu-id="851f1-163">On the Overview tab, click **Edit query**.</span></span>

    ![Edit Query](./media/iot-accelerators-integrate-data-lake/stream-analytics-edit-query.png)

1. <span data-ttu-id="851f1-165">In the Query editor, replace the [YourOutputAlias] and [YourInputAlias] placeholders with the values you defined previously.</span><span class="sxs-lookup"><span data-stu-id="851f1-165">In the Query editor, replace the [YourOutputAlias] and [YourInputAlias] placeholders with the values you defined previously.</span></span>

    ```sql
    SELECT
        *, System.Timestamp as time
    INTO
        DataLakeStore
    FROM
        IoTHub
    ```

    ![Stream Analytics Query](./media/iot-accelerators-integrate-data-lake/stream-analytics-query.png)

1. <span data-ttu-id="851f1-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="851f1-167">Click **Save**.</span></span>
1. <span data-ttu-id="851f1-168">Click **Yes** to accept the changes.</span><span class="sxs-lookup"><span data-stu-id="851f1-168">Click **Yes** to accept the changes.</span></span>

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="851f1-169">Start the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="851f1-169">Start the Stream Analytics job</span></span>

1. <span data-ttu-id="851f1-170">On the Overview tab, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="851f1-170">On the Overview tab, click **Start**.</span></span>

    ![Start Stream Analytics Job](./media/iot-accelerators-integrate-data-lake/stream-analytics-start.png)

1. <span data-ttu-id="851f1-172">On the Start job tab, click **Custom**.</span><span class="sxs-lookup"><span data-stu-id="851f1-172">On the Start job tab, click **Custom**.</span></span>

1. <span data-ttu-id="851f1-173">Set custom time to go back a few hours to pick up data from when your device has started streaming.</span><span class="sxs-lookup"><span data-stu-id="851f1-173">Set custom time to go back a few hours to pick up data from when your device has started streaming.</span></span>

1. <span data-ttu-id="851f1-174">Click **Start**.</span><span class="sxs-lookup"><span data-stu-id="851f1-174">Click **Start**.</span></span>

    ![Pick Custom Date](./media/iot-accelerators-integrate-data-lake/stream-analytics-start-custom.png)

    <span data-ttu-id="851f1-176">Wait until job goes into running state, if you see errors it could be from your query, make sure to verify that the syntax is correct.</span><span class="sxs-lookup"><span data-stu-id="851f1-176">Wait until job goes into running state, if you see errors it could be from your query, make sure to verify that the syntax is correct.</span></span>

    ![Job running](./media/iot-accelerators-integrate-data-lake/stream-analytics-running.png)

    <span data-ttu-id="851f1-178">The streaming job will begin to read data from your IoT Hub and store the data in your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-178">The streaming job will begin to read data from your IoT Hub and store the data in your Data Lake Store.</span></span> <span data-ttu-id="851f1-179">It may take a few minutes for the data to begin to appear in your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-179">It may take a few minutes for the data to begin to appear in your Data Lake Store.</span></span>

## <a name="explore-the-streaming-data"></a><span data-ttu-id="851f1-180">Explore the streaming data</span><span class="sxs-lookup"><span data-stu-id="851f1-180">Explore the streaming data</span></span>

1. <span data-ttu-id="851f1-181">Go to your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="851f1-181">Go to your Data Lake Store.</span></span>

1. <span data-ttu-id="851f1-182">On the Overview tab, click **Data explorer**.</span><span class="sxs-lookup"><span data-stu-id="851f1-182">On the Overview tab, click **Data explorer**.</span></span>

1. <span data-ttu-id="851f1-183">In the Data explorer, drill down to the **/streaming** folder.</span><span class="sxs-lookup"><span data-stu-id="851f1-183">In the Data explorer, drill down to the **/streaming** folder.</span></span> <span data-ttu-id="851f1-184">You will see folders created with YYYY/MM/DD/HH format.</span><span class="sxs-lookup"><span data-stu-id="851f1-184">You will see folders created with YYYY/MM/DD/HH format.</span></span>

    ![Explore Streaming Data](./media/iot-accelerators-integrate-data-lake/data-lake-store-data-explorer.png)

    <span data-ttu-id="851f1-186">You will see json files with one file per hour.</span><span class="sxs-lookup"><span data-stu-id="851f1-186">You will see json files with one file per hour.</span></span>

    ![Explore Streaming Data](./media/iot-accelerators-integrate-data-lake/data-lake-store-file-preview.png)

## <a name="next-steps"></a><span data-ttu-id="851f1-188">Next Steps</span><span class="sxs-lookup"><span data-stu-id="851f1-188">Next Steps</span></span>

<span data-ttu-id="851f1-189">Azure Data Lake Analytics can be used to perform big data analysis on your Data Lake Store data sets.</span><span class="sxs-lookup"><span data-stu-id="851f1-189">Azure Data Lake Analytics can be used to perform big data analysis on your Data Lake Store data sets.</span></span> <span data-ttu-id="851f1-190">Learn more on the [Data Lake Analytics Documentation](https://docs.microsoft.com/azure/data-lake-analytics).</span><span class="sxs-lookup"><span data-stu-id="851f1-190">Learn more on the [Data Lake Analytics Documentation](https://docs.microsoft.com/azure/data-lake-analytics).</span></span>
