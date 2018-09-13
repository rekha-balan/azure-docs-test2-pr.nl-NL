---
title: Query Avro data by using Azure Data Lake Analytics | Microsoft Docs
description: Use message body properties to route device telemetry to Blob storage and query the Avro format data that's written to Blob storage.
author: ash2017
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: asrastog
ms.openlocfilehash: a17df39c55b5c02c83e3f0b74a91d7109ddb4d3d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969003"
---
# <a name="query-avro-data-by-using-azure-data-lake-analytics"></a><span data-ttu-id="fa43c-103">Query Avro data by using Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fa43c-103">Query Avro data by using Azure Data Lake Analytics</span></span>

<span data-ttu-id="fa43c-104">This article discusses how to query Avro data to efficiently route messages from Azure IoT Hub to Azure services.</span><span class="sxs-lookup"><span data-stu-id="fa43c-104">This article discusses how to query Avro data to efficiently route messages from Azure IoT Hub to Azure services.</span></span> <span data-ttu-id="fa43c-105">As we announced in the blog post [Azure IoT Hub message routing: now with routing on message body], IoT Hub supports routing on either properties or the message body.</span><span class="sxs-lookup"><span data-stu-id="fa43c-105">As we announced in the blog post [Azure IoT Hub message routing: now with routing on message body], IoT Hub supports routing on either properties or the message body.</span></span> <span data-ttu-id="fa43c-106">For more information, see [Routing on message bodies][Routing on message bodies].</span><span class="sxs-lookup"><span data-stu-id="fa43c-106">For more information, see [Routing on message bodies][Routing on message bodies].</span></span> 

<span data-ttu-id="fa43c-107">The challenge has been that when Azure IoT Hub routes messages to Azure Blob storage, IoT Hub writes the content in Avro format, which has both a message body property and a message property.</span><span class="sxs-lookup"><span data-stu-id="fa43c-107">The challenge has been that when Azure IoT Hub routes messages to Azure Blob storage, IoT Hub writes the content in Avro format, which has both a message body property and a message property.</span></span> <span data-ttu-id="fa43c-108">IoT Hub supports writing data to Blob storage only in the Avro data format, and this format is not used for any other endpoints.</span><span class="sxs-lookup"><span data-stu-id="fa43c-108">IoT Hub supports writing data to Blob storage only in the Avro data format, and this format is not used for any other endpoints.</span></span> <span data-ttu-id="fa43c-109">For more information, see [When using Azure Storage containers][When using Azure storage containers].</span><span class="sxs-lookup"><span data-stu-id="fa43c-109">For more information, see [When using Azure Storage containers][When using Azure storage containers].</span></span> <span data-ttu-id="fa43c-110">Although the Avro format is great for data and message preservation, it's a challenge to use it to query data.</span><span class="sxs-lookup"><span data-stu-id="fa43c-110">Although the Avro format is great for data and message preservation, it's a challenge to use it to query data.</span></span> <span data-ttu-id="fa43c-111">In comparison, JSON or CSV format is much easier for querying data.</span><span class="sxs-lookup"><span data-stu-id="fa43c-111">In comparison, JSON or CSV format is much easier for querying data.</span></span>

<span data-ttu-id="fa43c-112">To address non-relational big-data needs and formats and overcome this challenge, you can use many of the big-data patterns for both transforming and scaling data.</span><span class="sxs-lookup"><span data-stu-id="fa43c-112">To address non-relational big-data needs and formats and overcome this challenge, you can use many of the big-data patterns for both transforming and scaling data.</span></span> <span data-ttu-id="fa43c-113">One of the patterns, “pay per query,” is Azure Data Lake Analytics, which is the focus of this article.</span><span class="sxs-lookup"><span data-stu-id="fa43c-113">One of the patterns, “pay per query,” is Azure Data Lake Analytics, which is the focus of this article.</span></span> <span data-ttu-id="fa43c-114">Although you can easily execute the query in Hadoop or other solutions, Data Lake Analytics is often better suited for this “pay per query” approach.</span><span class="sxs-lookup"><span data-stu-id="fa43c-114">Although you can easily execute the query in Hadoop or other solutions, Data Lake Analytics is often better suited for this “pay per query” approach.</span></span> 

<span data-ttu-id="fa43c-115">There is an “extractor” for Avro in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa43c-115">There is an “extractor” for Avro in U-SQL.</span></span> <span data-ttu-id="fa43c-116">For more information, see [U-SQL Avro example].</span><span class="sxs-lookup"><span data-stu-id="fa43c-116">For more information, see [U-SQL Avro example].</span></span>

## <a name="query-and-export-avro-data-to-a-csv-file"></a><span data-ttu-id="fa43c-117">Query and export Avro data to a CSV file</span><span class="sxs-lookup"><span data-stu-id="fa43c-117">Query and export Avro data to a CSV file</span></span>
<span data-ttu-id="fa43c-118">In this section, you query Avro data and export it to a CSV file in Azure Blob storage, although you could easily place the data in other repositories or data stores.</span><span class="sxs-lookup"><span data-stu-id="fa43c-118">In this section, you query Avro data and export it to a CSV file in Azure Blob storage, although you could easily place the data in other repositories or data stores.</span></span>

1. <span data-ttu-id="fa43c-119">Set up Azure IoT Hub to route data to an Azure Blob storage endpoint by using a property in the message body to select messages.</span><span class="sxs-lookup"><span data-stu-id="fa43c-119">Set up Azure IoT Hub to route data to an Azure Blob storage endpoint by using a property in the message body to select messages.</span></span>

    ![The "Custom endpoints" section][img-query-avro-data-1a]

    ![The Routes command][img-query-avro-data-1b]

2. <span data-ttu-id="fa43c-122">Ensure that your device has the encoding, content type, and needed data in either the properties or the message body, as referenced in the product documentation.</span><span class="sxs-lookup"><span data-stu-id="fa43c-122">Ensure that your device has the encoding, content type, and needed data in either the properties or the message body, as referenced in the product documentation.</span></span> <span data-ttu-id="fa43c-123">When you view these attributes in Device Explorer, as shown here, you can verify that they are set correctly.</span><span class="sxs-lookup"><span data-stu-id="fa43c-123">When you view these attributes in Device Explorer, as shown here, you can verify that they are set correctly.</span></span>

    ![The Event Hub Data pane][img-query-avro-data-2]

3. <span data-ttu-id="fa43c-125">Set up an Azure Data Lake Store instance and a Data Lake Analytics instance.</span><span class="sxs-lookup"><span data-stu-id="fa43c-125">Set up an Azure Data Lake Store instance and a Data Lake Analytics instance.</span></span> <span data-ttu-id="fa43c-126">Azure IoT Hub does not route to a Data Lake Store instance, but a Data Lake Analytics instance requires one.</span><span class="sxs-lookup"><span data-stu-id="fa43c-126">Azure IoT Hub does not route to a Data Lake Store instance, but a Data Lake Analytics instance requires one.</span></span>

    ![Data Lake Store and Data Lake Analytics instances][img-query-avro-data-3]

4. <span data-ttu-id="fa43c-128">In Data Lake Analytics, configure Azure Blob storage as an additional store, the same Blob storage that Azure IoT Hub routes data to.</span><span class="sxs-lookup"><span data-stu-id="fa43c-128">In Data Lake Analytics, configure Azure Blob storage as an additional store, the same Blob storage that Azure IoT Hub routes data to.</span></span>

    ![The "Data sources" pane][img-query-avro-data-4]
 
5. <span data-ttu-id="fa43c-130">As discussed in [U-SQL Avro example], you need four DLL files.</span><span class="sxs-lookup"><span data-stu-id="fa43c-130">As discussed in [U-SQL Avro example], you need four DLL files.</span></span> <span data-ttu-id="fa43c-131">Upload these files to a location in your Data Lake Store instance.</span><span class="sxs-lookup"><span data-stu-id="fa43c-131">Upload these files to a location in your Data Lake Store instance.</span></span>

    ![Four uploaded DLL files][img-query-avro-data-5] 

6. <span data-ttu-id="fa43c-133">In Visual Studio, create a U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="fa43c-133">In Visual Studio, create a U-SQL project.</span></span>
 
    ![Create a U-SQL project][img-query-avro-data-6]

7. <span data-ttu-id="fa43c-135">Paste the content of the following script into the newly created file.</span><span class="sxs-lookup"><span data-stu-id="fa43c-135">Paste the content of the following script into the newly created file.</span></span> <span data-ttu-id="fa43c-136">Modify the three highlighted sections: your Data Lake Analytics account, the associated DLL file paths, and the correct path for your storage account.</span><span class="sxs-lookup"><span data-stu-id="fa43c-136">Modify the three highlighted sections: your Data Lake Analytics account, the associated DLL file paths, and the correct path for your storage account.</span></span>
    
    ![The three sections to be modified][img-query-avro-data-7a]

    <span data-ttu-id="fa43c-138">The actual U-SQL script for simple output to a CSV file:</span><span class="sxs-lookup"><span data-stu-id="fa43c-138">The actual U-SQL script for simple output to a CSV file:</span></span>
    
    ```sql
        DROP ASSEMBLY IF EXISTS [Avro];
        CREATE ASSEMBLY [Avro] FROM @"/Assemblies/Avro/Avro.dll";
        DROP ASSEMBLY IF EXISTS [Microsoft.Analytics.Samples.Formats];
        CREATE ASSEMBLY [Microsoft.Analytics.Samples.Formats] FROM @"/Assemblies/Avro/Microsoft.Analytics.Samples.Formats.dll";
        DROP ASSEMBLY IF EXISTS [Newtonsoft.Json];
        CREATE ASSEMBLY [Newtonsoft.Json] FROM @"/Assemblies/Avro/Newtonsoft.Json.dll";
        DROP ASSEMBLY IF EXISTS [log4net];
        CREATE ASSEMBLY [log4net] FROM @"/Assemblies/Avro/log4net.dll";

        REFERENCE ASSEMBLY [Newtonsoft.Json];
        REFERENCE ASSEMBLY [log4net];
        REFERENCE ASSEMBLY [Avro];
        REFERENCE ASSEMBLY [Microsoft.Analytics.Samples.Formats];

        // Blob container storage account filenames, with any path
        DECLARE @input_file string = @"wasb://hottubrawdata@kevinsayazstorage/kevinsayIoT/{*}/{*}/{*}/{*}/{*}/{*}";
        DECLARE @output_file string = @"/output/output.csv";

        @rs =
        EXTRACT
        EnqueuedTimeUtc string,
        Body byte[]
        FROM @input_file

        USING new Microsoft.Analytics.Samples.Formats.ApacheAvro.AvroExtractor(@"
        {
        ""type"":""record"",
        ""name"":""Message"",
        ""namespace"":""Microsoft.Azure.Devices"",
        ""fields"":[{
        ""name"":""EnqueuedTimeUtc"",
        ""type"":""string""
        },
        {
        ""name"":""Properties"",
        ""type"":{
        ""type"":""map"",
        ""values"":""string""
        }
        },
        {
        ""name"":""SystemProperties"",
        ""type"":{
        ""type"":""map"",
        ""values"":""string""
        }
        },
        {
        ""name"":""Body"",
        ""type"":[""null"",""bytes""]
        }
        ]
        }");

        @cnt =
        SELECT EnqueuedTimeUtc AS time, Encoding.UTF8.GetString(Body) AS jsonmessage
        FROM @rs;

        OUTPUT @cnt TO @output_file USING Outputters.Text(); 
    ```    

    <span data-ttu-id="fa43c-139">It took Data Lake Analytics five minutes to run the following script, which was limited to 10 analytic units and processed 177 files.</span><span class="sxs-lookup"><span data-stu-id="fa43c-139">It took Data Lake Analytics five minutes to run the following script, which was limited to 10 analytic units and processed 177 files.</span></span> <span data-ttu-id="fa43c-140">The result is shown in the CSV-file output that's displayed in the following image:</span><span class="sxs-lookup"><span data-stu-id="fa43c-140">The result is shown in the CSV-file output that's displayed in the following image:</span></span>
    
    ![Results of the output to CSV file][img-query-avro-data-7b]

    ![Output converted to CSV file][img-query-avro-data-7c]

    <span data-ttu-id="fa43c-143">To parse the JSON, continue to step 8.</span><span class="sxs-lookup"><span data-stu-id="fa43c-143">To parse the JSON, continue to step 8.</span></span>
    
8. <span data-ttu-id="fa43c-144">Most IoT messages are in JSON file format.</span><span class="sxs-lookup"><span data-stu-id="fa43c-144">Most IoT messages are in JSON file format.</span></span> <span data-ttu-id="fa43c-145">By adding the following lines, you can parse the message into a JSON file, which lets you add the WHERE clauses and output only the needed data.</span><span class="sxs-lookup"><span data-stu-id="fa43c-145">By adding the following lines, you can parse the message into a JSON file, which lets you add the WHERE clauses and output only the needed data.</span></span>

    ```sql
       @jsonify = SELECT Microsoft.Analytics.Samples.Formats.Json.JsonFunctions.JsonTuple(Encoding.UTF8.GetString(Body)) AS message FROM @rs;
    
        /*
        @cnt =
            SELECT EnqueuedTimeUtc AS time, Encoding.UTF8.GetString(Body) AS jsonmessage
            FROM @rs;
        
        OUTPUT @cnt TO @output_file USING Outputters.Text();
        */
        
        @cnt =
            SELECT message["message"] AS iotmessage,
                   message["event"] AS msgevent,
                   message["object"] AS msgobject,
                   message["status"] AS msgstatus,
                   message["host"] AS msghost
            FROM @jsonify;
            
        OUTPUT @cnt TO @output_file USING Outputters.Text();
    ```

    <span data-ttu-id="fa43c-146">The output displays a column for each item in the `SELECT` command.</span><span class="sxs-lookup"><span data-stu-id="fa43c-146">The output displays a column for each item in the `SELECT` command.</span></span> 
    
    ![Output showing a column for each item][img-query-avro-data-8]

## <a name="next-steps"></a><span data-ttu-id="fa43c-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa43c-148">Next steps</span></span>
<span data-ttu-id="fa43c-149">In this tutorial, you learned how to query Avro data to efficiently route messages from Azure IoT Hub to Azure services.</span><span class="sxs-lookup"><span data-stu-id="fa43c-149">In this tutorial, you learned how to query Avro data to efficiently route messages from Azure IoT Hub to Azure services.</span></span>

<span data-ttu-id="fa43c-150">For examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator][lnk-iot-sa-land].</span><span class="sxs-lookup"><span data-stu-id="fa43c-150">For examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator][lnk-iot-sa-land].</span></span>

<span data-ttu-id="fa43c-151">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="fa43c-151">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="fa43c-152">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="fa43c-152">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images -->
[img-query-avro-data-1a]: ./media/iot-hub-query-avro-data/query-avro-data-1a.png
[img-query-avro-data-1b]: ./media/iot-hub-query-avro-data/query-avro-data-1b.png
[img-query-avro-data-2]: ./media/iot-hub-query-avro-data/query-avro-data-2.png
[img-query-avro-data-3]: ./media/iot-hub-query-avro-data/query-avro-data-3.png
[img-query-avro-data-4]: ./media/iot-hub-query-avro-data/query-avro-data-4.png
[img-query-avro-data-5]: ./media/iot-hub-query-avro-data/query-avro-data-5.png
[img-query-avro-data-6]: ./media/iot-hub-query-avro-data/query-avro-data-6.png
[img-query-avro-data-7a]: ./media/iot-hub-query-avro-data/query-avro-data-7a.png
[img-query-avro-data-7b]: ./media/iot-hub-query-avro-data/query-avro-data-7b.png
[img-query-avro-data-7c]: ./media/iot-hub-query-avro-data/query-avro-data-7c.png
[img-query-avro-data-8]: ./media/iot-hub-query-avro-data/query-avro-data-8.png

<!-- Links -->
[Azure IoT Hub message routing: now with routing on message body]: https://azure.microsoft.com/blog/iot-hub-message-routing-now-with-routing-on-message-body/

[Routing on message bodies]: iot-hub-devguide-query-language.md#routing-on-message-bodies
[When using Azure storage containers]:iot-hub-devguide-endpoints.md#when-using-azure-storage-containers

[U-SQL Avro example]:https://github.com/Azure/usql/tree/master/Examples/AvroExamples

[lnk-iot-sa-land]: ../iot-accelerators/index.yml
[IoT Hub developer guide]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
