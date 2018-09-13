## <a name="typical-output"></a><span data-ttu-id="144fe-101">Typical output</span><span class="sxs-lookup"><span data-stu-id="144fe-101">Typical output</span></span>

<span data-ttu-id="144fe-102">The following is an example of the output written to the log file by the Hello World sample.</span><span class="sxs-lookup"><span data-stu-id="144fe-102">The following is an example of the output written to the log file by the Hello World sample.</span></span> <span data-ttu-id="144fe-103">The output is formatted for legibility:</span><span class="sxs-lookup"><span data-stu-id="144fe-103">The output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="144fe-104">Code snippets</span><span class="sxs-lookup"><span data-stu-id="144fe-104">Code snippets</span></span>

<span data-ttu-id="144fe-105">This section discusses some key sections of the code in the hello\_world sample.</span><span class="sxs-lookup"><span data-stu-id="144fe-105">This section discusses some key sections of the code in the hello\_world sample.</span></span>

### <a name="gateway-creation"></a><span data-ttu-id="144fe-106">Gateway creation</span><span class="sxs-lookup"><span data-stu-id="144fe-106">Gateway creation</span></span>

<span data-ttu-id="144fe-107">The developer must write the *gateway process*.</span><span class="sxs-lookup"><span data-stu-id="144fe-107">The developer must write the *gateway process*.</span></span> <span data-ttu-id="144fe-108">This program creates the internal infrastructure (the broker), loads the modules, and sets everything up to function correctly.</span><span class="sxs-lookup"><span data-stu-id="144fe-108">This program creates the internal infrastructure (the broker), loads the modules, and sets everything up to function correctly.</span></span> <span data-ttu-id="144fe-109">The SDK provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span><span class="sxs-lookup"><span data-stu-id="144fe-109">The SDK provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="144fe-110">To use the **Gateway\_Create\_From\_JSON** function, you must pass it the path to a JSON file that specifies the modules to load.</span><span class="sxs-lookup"><span data-stu-id="144fe-110">To use the **Gateway\_Create\_From\_JSON** function, you must pass it the path to a JSON file that specifies the modules to load.</span></span>

<span data-ttu-id="144fe-111">You can find the code for the gateway process in the Hello World sample in the [main.c][lnk-main-c] file.</span><span class="sxs-lookup"><span data-stu-id="144fe-111">You can find the code for the gateway process in the Hello World sample in the [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="144fe-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span><span class="sxs-lookup"><span data-stu-id="144fe-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span></span> <span data-ttu-id="144fe-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span><span class="sxs-lookup"><span data-stu-id="144fe-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="144fe-114">The JSON settings file contains a list of modules to load and the links between the modules.</span><span class="sxs-lookup"><span data-stu-id="144fe-114">The JSON settings file contains a list of modules to load and the links between the modules.</span></span> <span data-ttu-id="144fe-115">Each module must specify a:</span><span class="sxs-lookup"><span data-stu-id="144fe-115">Each module must specify a:</span></span>

* <span data-ttu-id="144fe-116">**name**: a unique name for the module.</span><span class="sxs-lookup"><span data-stu-id="144fe-116">**name**: a unique name for the module.</span></span>
* <span data-ttu-id="144fe-117">**loader**: a loader that knows how to load the desired module.</span><span class="sxs-lookup"><span data-stu-id="144fe-117">**loader**: a loader that knows how to load the desired module.</span></span> <span data-ttu-id="144fe-118">Loaders are an extension point for loading different types of modules.</span><span class="sxs-lookup"><span data-stu-id="144fe-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="144fe-119">We provide loaders for use with modules written in native C, Node.js, Java, and .NET.</span><span class="sxs-lookup"><span data-stu-id="144fe-119">We provide loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="144fe-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use modules written in different languages, see the [Node.js](https://github.com/Azure/azure-iot-gateway-sdk/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/dotnet_binding_sample) samples.</span><span class="sxs-lookup"><span data-stu-id="144fe-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use modules written in different languages, see the [Node.js](https://github.com/Azure/azure-iot-gateway-sdk/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="144fe-121">**name**: name of the loader used to load the module.</span><span class="sxs-lookup"><span data-stu-id="144fe-121">**name**: name of the loader used to load the module.</span></span>
    * <span data-ttu-id="144fe-122">**entrypoint**: the path to the library containing the module.</span><span class="sxs-lookup"><span data-stu-id="144fe-122">**entrypoint**: the path to the library containing the module.</span></span> <span data-ttu-id="144fe-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span><span class="sxs-lookup"><span data-stu-id="144fe-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="144fe-124">The entry point is specific to the type of loader being used.</span><span class="sxs-lookup"><span data-stu-id="144fe-124">The entry point is specific to the type of loader being used.</span></span> <span data-ttu-id="144fe-125">The Node.js loader's entry point is a .js file.</span><span class="sxs-lookup"><span data-stu-id="144fe-125">The Node.js loader's entry point is a .js file.</span></span> <span data-ttu-id="144fe-126">The Java loader's entry point is a classpath plus a class name.</span><span class="sxs-lookup"><span data-stu-id="144fe-126">The Java loader's entry point is a classpath plus a class name.</span></span> <span data-ttu-id="144fe-127">The .NET loader's entry point is an assembly name plus a class name.</span><span class="sxs-lookup"><span data-stu-id="144fe-127">The .NET loader's entry point is an assembly name plus a class name.</span></span>

* <span data-ttu-id="144fe-128">**args**: any configuration information the module needs.</span><span class="sxs-lookup"><span data-stu-id="144fe-128">**args**: any configuration information the module needs.</span></span>

<span data-ttu-id="144fe-129">The following code shows the JSON used to declare all the modules for the Hello World sample on Linux.</span><span class="sxs-lookup"><span data-stu-id="144fe-129">The following code shows the JSON used to declare all the modules for the Hello World sample on Linux.</span></span> <span data-ttu-id="144fe-130">Whether a module requires any arguments depends on the design of the module.</span><span class="sxs-lookup"><span data-stu-id="144fe-130">Whether a module requires any arguments depends on the design of the module.</span></span> <span data-ttu-id="144fe-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span><span class="sxs-lookup"><span data-stu-id="144fe-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="144fe-132">The JSON file also contains the links between the modules that are passed to the broker.</span><span class="sxs-lookup"><span data-stu-id="144fe-132">The JSON file also contains the links between the modules that are passed to the broker.</span></span> <span data-ttu-id="144fe-133">A link has two properties:</span><span class="sxs-lookup"><span data-stu-id="144fe-133">A link has two properties:</span></span>

* <span data-ttu-id="144fe-134">**source**: a module name from the `modules` section, or "\*".</span><span class="sxs-lookup"><span data-stu-id="144fe-134">**source**: a module name from the `modules` section, or "\*".</span></span>
* <span data-ttu-id="144fe-135">**sink**: a module name from the `modules` section.</span><span class="sxs-lookup"><span data-stu-id="144fe-135">**sink**: a module name from the `modules` section.</span></span>

<span data-ttu-id="144fe-136">Each link defines a message route and direction.</span><span class="sxs-lookup"><span data-stu-id="144fe-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="144fe-137">Messages from module `source` are delivered to the module `sink`.</span><span class="sxs-lookup"><span data-stu-id="144fe-137">Messages from module `source` are delivered to the module `sink`.</span></span> <span data-ttu-id="144fe-138">The `source` may be set to "\*", indicating that messages from any module are received by `sink`.</span><span class="sxs-lookup"><span data-stu-id="144fe-138">The `source` may be set to "\*", indicating that messages from any module are received by `sink`.</span></span>

<span data-ttu-id="144fe-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span><span class="sxs-lookup"><span data-stu-id="144fe-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span></span> <span data-ttu-id="144fe-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span><span class="sxs-lookup"><span data-stu-id="144fe-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="144fe-141">Hello\_world module message publishing</span><span class="sxs-lookup"><span data-stu-id="144fe-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="144fe-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span><span class="sxs-lookup"><span data-stu-id="144fe-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="144fe-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span><span class="sxs-lookup"><span data-stu-id="144fe-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="144fe-144">Hello\_world module message processing</span><span class="sxs-lookup"><span data-stu-id="144fe-144">Hello\_world module message processing</span></span>

<span data-ttu-id="144fe-145">The hello\_world module never processes messages that other modules publish to the broker.</span><span class="sxs-lookup"><span data-stu-id="144fe-145">The hello\_world module never processes messages that other modules publish to the broker.</span></span> <span data-ttu-id="144fe-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span><span class="sxs-lookup"><span data-stu-id="144fe-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="144fe-147">Logger module message publishing and processing</span><span class="sxs-lookup"><span data-stu-id="144fe-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="144fe-148">The logger module receives messages from the broker and writes them to a file.</span><span class="sxs-lookup"><span data-stu-id="144fe-148">The logger module receives messages from the broker and writes them to a file.</span></span> <span data-ttu-id="144fe-149">It never publishes any messages.</span><span class="sxs-lookup"><span data-stu-id="144fe-149">It never publishes any messages.</span></span> <span data-ttu-id="144fe-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span><span class="sxs-lookup"><span data-stu-id="144fe-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span></span>

<span data-ttu-id="144fe-151">The **Logger_Recieve** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span><span class="sxs-lookup"><span data-stu-id="144fe-151">The **Logger_Recieve** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span></span> <span data-ttu-id="144fe-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span><span class="sxs-lookup"><span data-stu-id="144fe-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="144fe-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="144fe-153">Next steps</span></span>

<span data-ttu-id="144fe-154">To learn about how to use the IoT Gateway SDK, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="144fe-154">To learn about how to use the IoT Gateway SDK, see the following articles:</span></span>

* <span data-ttu-id="144fe-155">[IoT Gateway SDK – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated].</span><span class="sxs-lookup"><span data-stu-id="144fe-155">[IoT Gateway SDK – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated].</span></span>
* <span data-ttu-id="144fe-156">[Azure IoT Gateway SDK][lnk-gateway-sdk] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="144fe-156">[Azure IoT Gateway SDK][lnk-gateway-sdk] on GitHub.</span></span>

<!-- Links -->
[lnk-main-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/modules/logger/src/logger.c
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk/
[lnk-gateway-simulated]: ../articles/iot-hub/iot-hub-linux-gateway-sdk-simulated-device.md