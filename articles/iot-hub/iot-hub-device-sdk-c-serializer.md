---
title: Azure IoT device SDK for C - Serializer | Microsoft Docs
description: How to use the Serializer library in the Azure IoT device SDK for C to create device apps that communicate with an IoT hub.
services: iot-hub
documentationcenter: ''
author: olivierbloch
manager: timlt
editor: ''
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 3e285e776bf2237bd94b19d9dd0c14b5ebe23125
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550772"
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="15929-103">Azure IoT device SDK for C – more about serializer</span><span class="sxs-lookup"><span data-stu-id="15929-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="15929-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="15929-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="15929-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="15929-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15929-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="15929-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span><span class="sxs-lookup"><span data-stu-id="15929-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="15929-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span><span class="sxs-lookup"><span data-stu-id="15929-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="15929-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span><span class="sxs-lookup"><span data-stu-id="15929-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="15929-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span><span class="sxs-lookup"><span data-stu-id="15929-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="15929-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="15929-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="15929-112">Everything described in this article is based on the **serializer** SDK samples.</span><span class="sxs-lookup"><span data-stu-id="15929-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="15929-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span><span class="sxs-lookup"><span data-stu-id="15929-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="15929-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="15929-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="15929-115">The modeling language</span><span class="sxs-lookup"><span data-stu-id="15929-115">The modeling language</span></span>
<span data-ttu-id="15929-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span><span class="sxs-lookup"><span data-stu-id="15929-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="15929-117">As you can see, the modeling language is based on C macros.</span><span class="sxs-lookup"><span data-stu-id="15929-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="15929-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="15929-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="15929-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span><span class="sxs-lookup"><span data-stu-id="15929-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="15929-120">What goes inside the namespace are model definitions.</span><span class="sxs-lookup"><span data-stu-id="15929-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="15929-121">In this case, there is a single model for an anemometer.</span><span class="sxs-lookup"><span data-stu-id="15929-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="15929-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15929-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="15929-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span><span class="sxs-lookup"><span data-stu-id="15929-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="15929-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span><span class="sxs-lookup"><span data-stu-id="15929-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="15929-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span><span class="sxs-lookup"><span data-stu-id="15929-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="15929-126">We'll cover that next.</span><span class="sxs-lookup"><span data-stu-id="15929-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="15929-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="15929-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="15929-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="15929-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="15929-129">Be aware that these terms may be used interchangeably in this article.</span><span class="sxs-lookup"><span data-stu-id="15929-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="15929-130">Supported data types</span><span class="sxs-lookup"><span data-stu-id="15929-130">Supported data types</span></span>
<span data-ttu-id="15929-131">The following data types are supported in models created with the **serializer** library:</span><span class="sxs-lookup"><span data-stu-id="15929-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="15929-132">Type</span><span class="sxs-lookup"><span data-stu-id="15929-132">Type</span></span> | <span data-ttu-id="15929-133">Description</span><span class="sxs-lookup"><span data-stu-id="15929-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15929-134">double</span><span class="sxs-lookup"><span data-stu-id="15929-134">double</span></span> |<span data-ttu-id="15929-135">double precision floating point number</span><span class="sxs-lookup"><span data-stu-id="15929-135">double precision floating point number</span></span> |
| <span data-ttu-id="15929-136">int</span><span class="sxs-lookup"><span data-stu-id="15929-136">int</span></span> |<span data-ttu-id="15929-137">32 bit integer</span><span class="sxs-lookup"><span data-stu-id="15929-137">32 bit integer</span></span> |
| <span data-ttu-id="15929-138">float</span><span class="sxs-lookup"><span data-stu-id="15929-138">float</span></span> |<span data-ttu-id="15929-139">single precision floating point number</span><span class="sxs-lookup"><span data-stu-id="15929-139">single precision floating point number</span></span> |
| <span data-ttu-id="15929-140">long</span><span class="sxs-lookup"><span data-stu-id="15929-140">long</span></span> |<span data-ttu-id="15929-141">long integer</span><span class="sxs-lookup"><span data-stu-id="15929-141">long integer</span></span> |
| <span data-ttu-id="15929-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="15929-142">int8\_t</span></span> |<span data-ttu-id="15929-143">8 bit integer</span><span class="sxs-lookup"><span data-stu-id="15929-143">8 bit integer</span></span> |
| <span data-ttu-id="15929-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="15929-144">int16\_t</span></span> |<span data-ttu-id="15929-145">16 bit integer</span><span class="sxs-lookup"><span data-stu-id="15929-145">16 bit integer</span></span> |
| <span data-ttu-id="15929-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="15929-146">int32\_t</span></span> |<span data-ttu-id="15929-147">32 bit integer</span><span class="sxs-lookup"><span data-stu-id="15929-147">32 bit integer</span></span> |
| <span data-ttu-id="15929-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="15929-148">int64\_t</span></span> |<span data-ttu-id="15929-149">64 bit integer</span><span class="sxs-lookup"><span data-stu-id="15929-149">64 bit integer</span></span> |
| <span data-ttu-id="15929-150">bool</span><span class="sxs-lookup"><span data-stu-id="15929-150">bool</span></span> |<span data-ttu-id="15929-151">boolean</span><span class="sxs-lookup"><span data-stu-id="15929-151">boolean</span></span> |
| <span data-ttu-id="15929-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="15929-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="15929-153">ASCII string</span><span class="sxs-lookup"><span data-stu-id="15929-153">ASCII string</span></span> |
| <span data-ttu-id="15929-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="15929-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="15929-155">date time offset</span><span class="sxs-lookup"><span data-stu-id="15929-155">date time offset</span></span> |
| <span data-ttu-id="15929-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="15929-156">EDM\_GUID</span></span> |<span data-ttu-id="15929-157">GUID</span><span class="sxs-lookup"><span data-stu-id="15929-157">GUID</span></span> |
| <span data-ttu-id="15929-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="15929-158">EDM\_BINARY</span></span> |<span data-ttu-id="15929-159">binary</span><span class="sxs-lookup"><span data-stu-id="15929-159">binary</span></span> |
| <span data-ttu-id="15929-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="15929-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="15929-161">complex data type</span><span class="sxs-lookup"><span data-stu-id="15929-161">complex data type</span></span> |

<span data-ttu-id="15929-162">Let’s start with the last data type.</span><span class="sxs-lookup"><span data-stu-id="15929-162">Let’s start with the last data type.</span></span> <span data-ttu-id="15929-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span><span class="sxs-lookup"><span data-stu-id="15929-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="15929-164">These groupings allow us to define a model that looks like this:</span><span class="sxs-lookup"><span data-stu-id="15929-164">These groupings allow us to define a model that looks like this:</span></span>

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

<span data-ttu-id="15929-165">Our model contains a single data event of type **TestType**.</span><span class="sxs-lookup"><span data-stu-id="15929-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="15929-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span><span class="sxs-lookup"><span data-stu-id="15929-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="15929-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span><span class="sxs-lookup"><span data-stu-id="15929-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

<span data-ttu-id="15929-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span><span class="sxs-lookup"><span data-stu-id="15929-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="15929-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

<span data-ttu-id="15929-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="15929-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="15929-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span><span class="sxs-lookup"><span data-stu-id="15929-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="15929-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="15929-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="15929-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="15929-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

<span data-ttu-id="15929-174">If you run this code, the following message is sent to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="15929-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="15929-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span><span class="sxs-lookup"><span data-stu-id="15929-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="15929-177">The values also exactly match those used in the code.</span><span class="sxs-lookup"><span data-stu-id="15929-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="15929-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="15929-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="15929-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span><span class="sxs-lookup"><span data-stu-id="15929-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="15929-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span><span class="sxs-lookup"><span data-stu-id="15929-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="15929-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span><span class="sxs-lookup"><span data-stu-id="15929-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="15929-182">However, he serialized JSON generated by the example above brings up an important point.</span><span class="sxs-lookup"><span data-stu-id="15929-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="15929-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span><span class="sxs-lookup"><span data-stu-id="15929-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="15929-184">That particular point is what we'll cover next.</span><span class="sxs-lookup"><span data-stu-id="15929-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="15929-185">More about serialization</span><span class="sxs-lookup"><span data-stu-id="15929-185">More about serialization</span></span>
<span data-ttu-id="15929-186">The previous section highlights an example of the output generated by the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="15929-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span><span class="sxs-lookup"><span data-stu-id="15929-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="15929-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span><span class="sxs-lookup"><span data-stu-id="15929-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="15929-189">First, let's provide some background on the scenario we're trying to address.</span><span class="sxs-lookup"><span data-stu-id="15929-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="15929-190">We want to model a thermostat that measures temperature and humidity.</span><span class="sxs-lookup"><span data-stu-id="15929-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="15929-191">Each piece of data is going to be sent to IoT Hub differently.</span><span class="sxs-lookup"><span data-stu-id="15929-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="15929-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="15929-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="15929-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span><span class="sxs-lookup"><span data-stu-id="15929-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="15929-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span><span class="sxs-lookup"><span data-stu-id="15929-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="15929-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="15929-195">Model 1</span></span>
<span data-ttu-id="15929-196">Here's the first version of a model that supports the previous scenario:</span><span class="sxs-lookup"><span data-stu-id="15929-196">Here's the first version of a model that supports the previous scenario:</span></span>

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

<span data-ttu-id="15929-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="15929-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="15929-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="15929-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="15929-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span><span class="sxs-lookup"><span data-stu-id="15929-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="15929-200">This model gives us a natural way to model the data for the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="15929-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="15929-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span><span class="sxs-lookup"><span data-stu-id="15929-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="15929-202">We can send a temperature event to the cloud using code such as the following:</span><span class="sxs-lookup"><span data-stu-id="15929-202">We can send a temperature event to the cloud using code such as the following:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span><span class="sxs-lookup"><span data-stu-id="15929-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="15929-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span><span class="sxs-lookup"><span data-stu-id="15929-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="15929-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span><span class="sxs-lookup"><span data-stu-id="15929-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="15929-206">The previous code serializes the temperature event into a buffer.</span><span class="sxs-lookup"><span data-stu-id="15929-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="15929-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

<span data-ttu-id="15929-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span><span class="sxs-lookup"><span data-stu-id="15929-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="15929-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="15929-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span><span class="sxs-lookup"><span data-stu-id="15929-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="15929-211">This is directly reflected in the serialized data.</span><span class="sxs-lookup"><span data-stu-id="15929-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="15929-212">Similarly, we can send a humidity event with this code:</span><span class="sxs-lookup"><span data-stu-id="15929-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-213">The serialized form that’s sent to IoT Hub appears as follows:</span><span class="sxs-lookup"><span data-stu-id="15929-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="15929-214">Again, this is as expected.</span><span class="sxs-lookup"><span data-stu-id="15929-214">Again, this is as expected.</span></span>

<span data-ttu-id="15929-215">With this model, you can imagine how additional events can easily be added.</span><span class="sxs-lookup"><span data-stu-id="15929-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="15929-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="15929-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="15929-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span><span class="sxs-lookup"><span data-stu-id="15929-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="15929-218">Model 2</span><span class="sxs-lookup"><span data-stu-id="15929-218">Model 2</span></span>
<span data-ttu-id="15929-219">Consider this alternative model to the one above:</span><span class="sxs-lookup"><span data-stu-id="15929-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="15929-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span><span class="sxs-lookup"><span data-stu-id="15929-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="15929-221">Just for the moment let’s ignore the **Time** event.</span><span class="sxs-lookup"><span data-stu-id="15929-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="15929-222">With that aside, here’s the code to ingress **Temperature**:</span><span class="sxs-lookup"><span data-stu-id="15929-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-223">This code sends the following serialized event to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="15929-224">And the code for sending the Humidity event appears as follows:</span><span class="sxs-lookup"><span data-stu-id="15929-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-225">This code sends this to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="15929-226">So far there are still no surprises.</span><span class="sxs-lookup"><span data-stu-id="15929-226">So far there are still no surprises.</span></span> <span data-ttu-id="15929-227">Now let's change how we use the SERIALIZE macro.</span><span class="sxs-lookup"><span data-stu-id="15929-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="15929-228">The **SERIALIZE** macro can take multiple data events as arguments.</span><span class="sxs-lookup"><span data-stu-id="15929-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="15929-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span><span class="sxs-lookup"><span data-stu-id="15929-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="15929-231">[</span><span class="sxs-lookup"><span data-stu-id="15929-231">[</span></span>

<span data-ttu-id="15929-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="15929-232">{"Temperature":75},</span></span>

<span data-ttu-id="15929-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="15929-233">{"Humidity":45}</span></span>

<span data-ttu-id="15929-234">]</span><span class="sxs-lookup"><span data-stu-id="15929-234">]</span></span>

<span data-ttu-id="15929-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span><span class="sxs-lookup"><span data-stu-id="15929-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="15929-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span><span class="sxs-lookup"><span data-stu-id="15929-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="15929-237">However, that’s not the case.</span><span class="sxs-lookup"><span data-stu-id="15929-237">However, that’s not the case.</span></span> <span data-ttu-id="15929-238">Instead, the code above sends this single data event to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="15929-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="15929-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="15929-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span><span class="sxs-lookup"><span data-stu-id="15929-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="15929-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span><span class="sxs-lookup"><span data-stu-id="15929-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="15929-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span><span class="sxs-lookup"><span data-stu-id="15929-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="15929-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span><span class="sxs-lookup"><span data-stu-id="15929-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="15929-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span><span class="sxs-lookup"><span data-stu-id="15929-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="15929-245">To make sense of this let’s go back to our model:</span><span class="sxs-lookup"><span data-stu-id="15929-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="15929-246">Think of this model in object-oriented terms.</span><span class="sxs-lookup"><span data-stu-id="15929-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="15929-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="15929-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="15929-248">We can send the entire state of our model with code such as the following:</span><span class="sxs-lookup"><span data-stu-id="15929-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="15929-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="15929-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="15929-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span><span class="sxs-lookup"><span data-stu-id="15929-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="15929-251">It’s useful to send only a subset of data events, such as in our earlier example:</span><span class="sxs-lookup"><span data-stu-id="15929-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="15929-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span><span class="sxs-lookup"><span data-stu-id="15929-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="15929-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span><span class="sxs-lookup"><span data-stu-id="15929-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="15929-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span><span class="sxs-lookup"><span data-stu-id="15929-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="15929-255">The best approach depends on you and how you think about your model.</span><span class="sxs-lookup"><span data-stu-id="15929-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="15929-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span><span class="sxs-lookup"><span data-stu-id="15929-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="15929-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="15929-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="15929-258">Then you send each event as we did in the first example above.</span><span class="sxs-lookup"><span data-stu-id="15929-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="15929-259">In this approach you would only pass a single data event to **SERIALIZER**.</span><span class="sxs-lookup"><span data-stu-id="15929-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="15929-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span><span class="sxs-lookup"><span data-stu-id="15929-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="15929-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span><span class="sxs-lookup"><span data-stu-id="15929-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="15929-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span><span class="sxs-lookup"><span data-stu-id="15929-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="15929-263">Nether approach is right or wrong.</span><span class="sxs-lookup"><span data-stu-id="15929-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="15929-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span><span class="sxs-lookup"><span data-stu-id="15929-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="15929-265">Message handling</span><span class="sxs-lookup"><span data-stu-id="15929-265">Message handling</span></span>
<span data-ttu-id="15929-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span><span class="sxs-lookup"><span data-stu-id="15929-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="15929-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="15929-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="15929-268">Recall from that article that you process messages by registering a message callback function:</span><span class="sxs-lookup"><span data-stu-id="15929-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="15929-269">You then write the callback function that’s invoked when a message is received:</span><span class="sxs-lookup"><span data-stu-id="15929-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="15929-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span><span class="sxs-lookup"><span data-stu-id="15929-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="15929-271">For example, if your model defines this action:</span><span class="sxs-lookup"><span data-stu-id="15929-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="15929-272">You must define a function with this signature:</span><span class="sxs-lookup"><span data-stu-id="15929-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="15929-273">**SetAirResistance** is then called when that message is sent to your device.</span><span class="sxs-lookup"><span data-stu-id="15929-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="15929-274">What we haven't explained yet is what the serialized version of message looks like.</span><span class="sxs-lookup"><span data-stu-id="15929-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="15929-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span><span class="sxs-lookup"><span data-stu-id="15929-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="15929-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span><span class="sxs-lookup"><span data-stu-id="15929-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="15929-277">You still need to know what string to send to invoke a particular action.</span><span class="sxs-lookup"><span data-stu-id="15929-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="15929-278">The general format for sending a message appears as follows:</span><span class="sxs-lookup"><span data-stu-id="15929-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="15929-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span><span class="sxs-lookup"><span data-stu-id="15929-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="15929-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span><span class="sxs-lookup"><span data-stu-id="15929-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="15929-281">The action name must exactly match an action defined in your model.</span><span class="sxs-lookup"><span data-stu-id="15929-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="15929-282">The parameter names must match as well.</span><span class="sxs-lookup"><span data-stu-id="15929-282">The parameter names must match as well.</span></span> <span data-ttu-id="15929-283">Also note case sensitivity.</span><span class="sxs-lookup"><span data-stu-id="15929-283">Also note case sensitivity.</span></span> <span data-ttu-id="15929-284">**Name** and **Parameters** are always uppercase.</span><span class="sxs-lookup"><span data-stu-id="15929-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="15929-285">Make sure to match the case of your action name and parameters in your model.</span><span class="sxs-lookup"><span data-stu-id="15929-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="15929-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="15929-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="15929-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span><span class="sxs-lookup"><span data-stu-id="15929-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="15929-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="15929-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span><span class="sxs-lookup"><span data-stu-id="15929-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="15929-290">Macro configuration</span><span class="sxs-lookup"><span data-stu-id="15929-290">Macro configuration</span></span>
<span data-ttu-id="15929-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span><span class="sxs-lookup"><span data-stu-id="15929-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="15929-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span><span class="sxs-lookup"><span data-stu-id="15929-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="15929-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="15929-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="15929-294">Within the shared utility library, you will find the following folder:</span><span class="sxs-lookup"><span data-stu-id="15929-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="15929-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="15929-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="15929-296">The program in this solution generates the **macro\_utils.h** file.</span><span class="sxs-lookup"><span data-stu-id="15929-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="15929-297">There’s a default macro\_utils.h file included with the SDK.</span><span class="sxs-lookup"><span data-stu-id="15929-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="15929-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span><span class="sxs-lookup"><span data-stu-id="15929-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="15929-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="15929-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="15929-300">These values are the default parameters included with the SDK.</span><span class="sxs-lookup"><span data-stu-id="15929-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="15929-301">Each parameter has the following meaning:</span><span class="sxs-lookup"><span data-stu-id="15929-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="15929-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span><span class="sxs-lookup"><span data-stu-id="15929-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="15929-303">nArithmetic – Controls the total number of members allowed in a model.</span><span class="sxs-lookup"><span data-stu-id="15929-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="15929-304">The reason these parameters are important is because they control how large your model can be.</span><span class="sxs-lookup"><span data-stu-id="15929-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="15929-305">For example, consider this model definition:</span><span class="sxs-lookup"><span data-stu-id="15929-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="15929-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span><span class="sxs-lookup"><span data-stu-id="15929-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="15929-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="15929-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="15929-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="15929-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="15929-309">Effectively, this defines how many data event and action declarations you can have.</span><span class="sxs-lookup"><span data-stu-id="15929-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="15929-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span><span class="sxs-lookup"><span data-stu-id="15929-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="15929-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span><span class="sxs-lookup"><span data-stu-id="15929-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="15929-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span><span class="sxs-lookup"><span data-stu-id="15929-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="15929-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span><span class="sxs-lookup"><span data-stu-id="15929-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="15929-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="15929-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="15929-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span><span class="sxs-lookup"><span data-stu-id="15929-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="15929-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span><span class="sxs-lookup"><span data-stu-id="15929-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="15929-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="15929-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="15929-318">This enables your code to compile against the source code of the serializer library.</span><span class="sxs-lookup"><span data-stu-id="15929-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="15929-319">This includes the updated macro\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="15929-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="15929-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span><span class="sxs-lookup"><span data-stu-id="15929-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="15929-321">Then add this project to your Visual Studio solution:</span><span class="sxs-lookup"><span data-stu-id="15929-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="15929-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="15929-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="15929-323">When you're done, your solution should look like this:</span><span class="sxs-lookup"><span data-stu-id="15929-323">When you're done, your solution should look like this:</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="15929-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span><span class="sxs-lookup"><span data-stu-id="15929-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="15929-325">Note that increasing these values high enough can exceed compiler limits.</span><span class="sxs-lookup"><span data-stu-id="15929-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="15929-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span><span class="sxs-lookup"><span data-stu-id="15929-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="15929-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span><span class="sxs-lookup"><span data-stu-id="15929-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="15929-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span><span class="sxs-lookup"><span data-stu-id="15929-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="15929-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span><span class="sxs-lookup"><span data-stu-id="15929-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="15929-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="15929-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span><span class="sxs-lookup"><span data-stu-id="15929-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="15929-332">The lower-level APIs</span><span class="sxs-lookup"><span data-stu-id="15929-332">The lower-level APIs</span></span>
<span data-ttu-id="15929-333">The sample application on which this article focused is **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="15929-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="15929-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span><span class="sxs-lookup"><span data-stu-id="15929-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="15929-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span><span class="sxs-lookup"><span data-stu-id="15929-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="15929-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span><span class="sxs-lookup"><span data-stu-id="15929-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="15929-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span><span class="sxs-lookup"><span data-stu-id="15929-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="15929-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="15929-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="15929-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="15929-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="15929-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="15929-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="15929-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="15929-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="15929-342">These APIs are demonstrated in **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="15929-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="15929-343">There is also an analogous set of lower-level APIs.</span><span class="sxs-lookup"><span data-stu-id="15929-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="15929-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="15929-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="15929-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="15929-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="15929-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="15929-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="15929-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="15929-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="15929-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span><span class="sxs-lookup"><span data-stu-id="15929-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="15929-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span><span class="sxs-lookup"><span data-stu-id="15929-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="15929-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15929-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="15929-351">Either set of APIs work equally well with the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="15929-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="15929-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span><span class="sxs-lookup"><span data-stu-id="15929-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="15929-353">Additional topics</span><span class="sxs-lookup"><span data-stu-id="15929-353">Additional topics</span></span>
<span data-ttu-id="15929-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span><span class="sxs-lookup"><span data-stu-id="15929-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="15929-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="15929-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="15929-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="15929-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="15929-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span><span class="sxs-lookup"><span data-stu-id="15929-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="15929-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span><span class="sxs-lookup"><span data-stu-id="15929-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="15929-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="15929-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="15929-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="15929-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="15929-361">A feature that is unique to the **serializer** library are the initialization APIs.</span><span class="sxs-lookup"><span data-stu-id="15929-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="15929-362">Before you can start working with the library, you must call **serializer\_init**:</span><span class="sxs-lookup"><span data-stu-id="15929-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="15929-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="15929-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="15929-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="15929-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="15929-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="15929-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="15929-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span><span class="sxs-lookup"><span data-stu-id="15929-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15929-367">Next steps</span><span class="sxs-lookup"><span data-stu-id="15929-367">Next steps</span></span>
<span data-ttu-id="15929-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15929-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="15929-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span><span class="sxs-lookup"><span data-stu-id="15929-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="15929-370">For additional information, there are a few samples in the SDK not covered here.</span><span class="sxs-lookup"><span data-stu-id="15929-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="15929-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span><span class="sxs-lookup"><span data-stu-id="15929-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="15929-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="15929-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="15929-373">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="15929-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="15929-374">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="15929-374">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md





