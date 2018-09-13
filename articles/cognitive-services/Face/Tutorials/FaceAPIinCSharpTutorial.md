---
title: Face API C# tutorial | Microsoft Docs
description: Create a simple Windows app that uses the Cognitive Services Emotion API to detect faces in an image by framing the faces.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 02/24/2017
ms.author: anroth
ms.openlocfilehash: 7d57d3fedcb65878404354b7c593188e0bad84b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550549"
---
# <a name="getting-started-with-face-api-in-c35-tutorial"></a><span data-ttu-id="bac1e-103">Getting Started with Face API in C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="bac1e-103">Getting Started with Face API in C&#35; Tutorial</span></span>

<span data-ttu-id="bac1e-104">In this tutorial, you will learn to create and develop a simple Windows application that invokes the Face API to detect faces in an image by framing the faces.</span><span class="sxs-lookup"><span data-stu-id="bac1e-104">In this tutorial, you will learn to create and develop a simple Windows application that invokes the Face API to detect faces in an image by framing the faces.</span></span>

![GettingStartCSharpScreenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/GetStartedCSharp-Detected.PNG)

## <a name="Preparation"></a><span data-ttu-id="bac1e-106">Preparation</span><span class="sxs-lookup"><span data-stu-id="bac1e-106">Preparation</span></span>

<span data-ttu-id="bac1e-107">To use the tutorial, you will need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="bac1e-107">To use the tutorial, you will need the following prerequisites:</span></span>

- <span data-ttu-id="bac1e-108">Make sure Visual Studio 2015 is installed.</span><span class="sxs-lookup"><span data-stu-id="bac1e-108">Make sure Visual Studio 2015 is installed.</span></span>

## <a name="step1"></a><span data-ttu-id="bac1e-109">Step 1: Subscribe for Face API and get your subscription key</span><span class="sxs-lookup"><span data-stu-id="bac1e-109">Step 1: Subscribe for Face API and get your subscription key</span></span>

<span data-ttu-id="bac1e-110">Before using any Face API, you must sign up to subscribe to Face API in the Microsoft Cognitive Services (formerly Project Oxford) portal.</span><span class="sxs-lookup"><span data-stu-id="bac1e-110">Before using any Face API, you must sign up to subscribe to Face API in the Microsoft Cognitive Services (formerly Project Oxford) portal.</span></span> <span data-ttu-id="bac1e-111">See [subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="bac1e-111">See [subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="bac1e-112">Both primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bac1e-112">Both primary and secondary key can be used in this tutorial.</span></span>

## <a name="step2"></a><span data-ttu-id="bac1e-113">Step 2: Create the application framework</span><span class="sxs-lookup"><span data-stu-id="bac1e-113">Step 2: Create the application framework</span></span>

<span data-ttu-id="bac1e-114">In this step you will create a Windows application project to implement the basic UI for picking up and displaying an image.</span><span class="sxs-lookup"><span data-stu-id="bac1e-114">In this step you will create a Windows application project to implement the basic UI for picking up and displaying an image.</span></span> <span data-ttu-id="bac1e-115">Simply follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="bac1e-115">Simply follow the instructions below:</span></span> 

1. <span data-ttu-id="bac1e-116">Open Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bac1e-116">Open Visual Studio 2015.</span></span>
2. <span data-ttu-id="bac1e-117">From the File menu, click New and then Project.</span><span class="sxs-lookup"><span data-stu-id="bac1e-117">From the File menu, click New and then Project.</span></span>
3. <span data-ttu-id="bac1e-118">In the New Project dialog box, click Visual C# &gt; Windows &gt; Classic Desktop &gt; WPF Application.</span><span class="sxs-lookup"><span data-stu-id="bac1e-118">In the New Project dialog box, click Visual C# &gt; Windows &gt; Classic Desktop &gt; WPF Application.</span></span>
4. <span data-ttu-id="bac1e-119">Name the application _MyFirstApp_, check the 'Create directory for solution' checkbox, name the solution _MyFirstAppSln_, and then click OK.</span><span class="sxs-lookup"><span data-stu-id="bac1e-119">Name the application _MyFirstApp_, check the 'Create directory for solution' checkbox, name the solution _MyFirstAppSln_, and then click OK.</span></span> 

![GettingStartCSharpNewProject](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/getstarted-image002.png)

5. <span data-ttu-id="bac1e-121">Locate the Solution Explorer, right click your project (MyFirstApp in this case) and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="bac1e-121">Locate the Solution Explorer, right click your project (MyFirstApp in this case) and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="bac1e-122">In NuGet Package Manager window, select nuget.org as your Package source, search for Newtonsoft.Json and install.</span><span class="sxs-lookup"><span data-stu-id="bac1e-122">In NuGet Package Manager window, select nuget.org as your Package source, search for Newtonsoft.Json and install.</span></span> 

![GettingStartCSharpPackageManager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/json.png)

7. <span data-ttu-id="bac1e-124">Open MainWindow.xaml, and replace the existing code with the following code to create the window UI:</span><span class="sxs-lookup"><span data-stu-id="bac1e-124">Open MainWindow.xaml, and replace the existing code with the following code to create the window UI:</span></span> 

        <Window x:Class="MyFirstApp.MainWindow"
                xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"       
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"        
                Title="MainWindow" Height="350" Width="450">        
            <Grid x:Name="BackPanel">    
                <Image x:Name="FacePhoto" Stretch="Uniform" Margin="0,0,0,30"/>        
                <Button x:Name="BrowseButton" Margin="20,5" Height="20"         
                        VerticalAlignment="Bottom" Content="Browse..."                
                        Click="BrowseButton_Click"/>                
            </Grid>    
        </Window>

8. <span data-ttu-id="bac1e-125">Open MainWindow.xaml.cs, and insert the following code inside the MainWindow class for the 'Browse' button:</span><span class="sxs-lookup"><span data-stu-id="bac1e-125">Open MainWindow.xaml.cs, and insert the following code inside the MainWindow class for the 'Browse' button:</span></span> 
        
        private void BrowseButton_Click(object sender, RoutedEventArgs e)
        {
            var openDlg = new Microsoft.Win32.OpenFileDialog();
        
            openDlg.Filter = "JPEG Image(*.jpg)|*.jpg";
            bool? result = openDlg.ShowDialog(this);
        
            if (!(bool)result)
            {
                return;
            }
        
            string filePath = openDlg.FileName;
        
            Uri fileUri = new Uri(filePath);
            BitmapImage bitmapSource = new BitmapImage();
        
            bitmapSource.BeginInit();
            bitmapSource.CacheOption = BitmapCacheOption.None;
            bitmapSource.UriSource = fileUri;
            bitmapSource.EndInit();
        
            FacePhoto.Source = bitmapSource;
        }

<span data-ttu-id="bac1e-126">Now your app can browse for a photo and display it in the window, similar to the image below:</span><span class="sxs-lookup"><span data-stu-id="bac1e-126">Now your app can browse for a photo and display it in the window, similar to the image below:</span></span> 

![GettingStartCSharpUI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/GetStartedCSharp-UI.PNG)

## <a name="step3"></a><span data-ttu-id="bac1e-128">Step 3: Configure the Face API client library</span><span class="sxs-lookup"><span data-stu-id="bac1e-128">Step 3: Configure the Face API client library</span></span>

<span data-ttu-id="bac1e-129">Face API is a cloud API which you can invoke through HTTPS requests.</span><span class="sxs-lookup"><span data-stu-id="bac1e-129">Face API is a cloud API which you can invoke through HTTPS requests.</span></span> <span data-ttu-id="bac1e-130">For a more convenient approach to using Face API in .NET platform applications, a client library is also provided to encapsulate the web requests.</span><span class="sxs-lookup"><span data-stu-id="bac1e-130">For a more convenient approach to using Face API in .NET platform applications, a client library is also provided to encapsulate the web requests.</span></span> <span data-ttu-id="bac1e-131">In this example, we use the client library to simplify our work.</span><span class="sxs-lookup"><span data-stu-id="bac1e-131">In this example, we use the client library to simplify our work.</span></span> <span data-ttu-id="bac1e-132">Follow the instructions below to configure the client library:</span><span class="sxs-lookup"><span data-stu-id="bac1e-132">Follow the instructions below to configure the client library:</span></span> 

1. <span data-ttu-id="bac1e-133">Locate the Solution Explorer, right click your project (MyFirstApp in this case) and then click Manage NuGet Packages.</span><span class="sxs-lookup"><span data-stu-id="bac1e-133">Locate the Solution Explorer, right click your project (MyFirstApp in this case) and then click Manage NuGet Packages.</span></span> 
2. <span data-ttu-id="bac1e-134">In the NuGet Package Manager window, select nuget.org as your Package source, search for Microsoft.ProjectOxford.Face and install.</span><span class="sxs-lookup"><span data-stu-id="bac1e-134">In the NuGet Package Manager window, select nuget.org as your Package source, search for Microsoft.ProjectOxford.Face and install.</span></span>  

![GettingStartCSharpPackageManagerSDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/face.png)  

3. <span data-ttu-id="bac1e-136">Check your project references, Microsoft.ProjectOxford.Face will be automatically added after the installation succeeds.</span><span class="sxs-lookup"><span data-stu-id="bac1e-136">Check your project references, Microsoft.ProjectOxford.Face will be automatically added after the installation succeeds.</span></span>

![GetStartedCSharp-CheckInstrallation.png](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/GetStartedCSharp-CheckInstallation.png)

4. <span data-ttu-id="bac1e-138">Open MainWindow.xaml.cs in your MyFirstApp project, add this using directives to the beginning of the file:      using System.IO;      using Microsoft.ProjectOxford.Face;      using Microsoft.ProjectOxford.Face.Contract;</span><span class="sxs-lookup"><span data-stu-id="bac1e-138">Open MainWindow.xaml.cs in your MyFirstApp project, add this using directives to the beginning of the file:      using System.IO;      using Microsoft.ProjectOxford.Face;      using Microsoft.ProjectOxford.Face.Contract;</span></span> 
5. <span data-ttu-id="bac1e-139">Insert the following code in the MainWindow class:      private readonly IFaceServiceClient faceServiceClient = new FaceServiceClient("_key_"); Replace the word _key_ with the subscription key you obtained in step 1.</span><span class="sxs-lookup"><span data-stu-id="bac1e-139">Insert the following code in the MainWindow class:      private readonly IFaceServiceClient faceServiceClient = new FaceServiceClient("_key_"); Replace the word _key_ with the subscription key you obtained in step 1.</span></span>
6. <span data-ttu-id="bac1e-140">Now you are ready to call the Face API from your application.</span><span class="sxs-lookup"><span data-stu-id="bac1e-140">Now you are ready to call the Face API from your application.</span></span> 

## <a name="step4"></a><span data-ttu-id="bac1e-141">Step 4: Upload images to detect faces</span><span class="sxs-lookup"><span data-stu-id="bac1e-141">Step 4: Upload images to detect faces</span></span>

<span data-ttu-id="bac1e-142">The most straightforward way to detect faces is by calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API by uploading the image file directly.</span><span class="sxs-lookup"><span data-stu-id="bac1e-142">The most straightforward way to detect faces is by calling the [Face - Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API by uploading the image file directly.</span></span>
<span data-ttu-id="bac1e-143">When using the client library, this can be done by using the asynchronous method DetectAsync of FaceServiceClient.</span><span class="sxs-lookup"><span data-stu-id="bac1e-143">When using the client library, this can be done by using the asynchronous method DetectAsync of FaceServiceClient.</span></span>
<span data-ttu-id="bac1e-144">Each returned face contains a rectangle to indicate its location, combined with a series of optional face attributes.</span><span class="sxs-lookup"><span data-stu-id="bac1e-144">Each returned face contains a rectangle to indicate its location, combined with a series of optional face attributes.</span></span>
<span data-ttu-id="bac1e-145">In this example, we only need to retrieve the face location.</span><span class="sxs-lookup"><span data-stu-id="bac1e-145">In this example, we only need to retrieve the face location.</span></span> <span data-ttu-id="bac1e-146">Here we need to insert an asynchronous function into the MainWindow class for face detection:</span><span class="sxs-lookup"><span data-stu-id="bac1e-146">Here we need to insert an asynchronous function into the MainWindow class for face detection:</span></span> 
```CSharp
private async Task<FaceRectangle[]> UploadAndDetectFaces(string imageFilePath)
{
    try
    {
        using (Stream imageFileStream = File.OpenRead(imageFilePath))
        {
            var faces = await faceServiceClient.DetectAsync(imageFileStream);
            var faceRects = faces.Select(face => face.FaceRectangle);
            return faceRects.ToArray();
        }
    }
    catch (Exception)
    {
        return new FaceRectangle[0];
    }
}
```

## <a name="step5"></a><span data-ttu-id="bac1e-147">Step 5: Mark faces in the image</span><span class="sxs-lookup"><span data-stu-id="bac1e-147">Step 5: Mark faces in the image</span></span>

<span data-ttu-id="bac1e-148">In this last step, we combine all the above steps and mark the detected faces in the image.</span><span class="sxs-lookup"><span data-stu-id="bac1e-148">In this last step, we combine all the above steps and mark the detected faces in the image.</span></span> <span data-ttu-id="bac1e-149">First, open MainWindow.xaml.cs and add the 'async' modifier to the BrowseButton_Click method:</span><span class="sxs-lookup"><span data-stu-id="bac1e-149">First, open MainWindow.xaml.cs and add the 'async' modifier to the BrowseButton_Click method:</span></span> 
```csharp
private async void BrowseButton_Click(object sender, RoutedEventArgs e)
```
<span data-ttu-id="bac1e-150">Now insert the following code at the end of the BrowseButton_Click event handler:</span><span class="sxs-lookup"><span data-stu-id="bac1e-150">Now insert the following code at the end of the BrowseButton_Click event handler:</span></span> 
```csharp
Title = "Detecting...";
FaceRectangle[] faceRects = await UploadAndDetectFaces(filePath);
Title = String.Format("Detection Finished. {0} face(s) detected", faceRects.Length);

if (faceRects.Length > 0)
{
    DrawingVisual visual = new DrawingVisual();
    DrawingContext drawingContext = visual.RenderOpen();
    drawingContext.DrawImage(bitmapSource,
        new Rect(0, 0, bitmapSource.Width, bitmapSource.Height));
    double dpi = bitmapSource.DpiX;
    double resizeFactor = 96 / dpi;

    foreach (var faceRect in faceRects)
    {
        drawingContext.DrawRectangle(
            Brushes.Transparent,
            new Pen(Brushes.Red, 2),
            new Rect(
                faceRect.Left * resizeFactor,
                faceRect.Top * resizeFactor,
                faceRect.Width * resizeFactor,
                faceRect.Height * resizeFactor
                )
        );
    }

    drawingContext.Close();
    RenderTargetBitmap faceWithRectBitmap = new RenderTargetBitmap(
        (int)(bitmapSource.PixelWidth * resizeFactor),
        (int)(bitmapSource.PixelHeight * resizeFactor),
        96,
        96,
        PixelFormats.Pbgra32);

    faceWithRectBitmap.Render(visual);
    FacePhoto.Source = faceWithRectBitmap;
}
```

<span data-ttu-id="bac1e-151">Run this application and browse for an image containing a face.</span><span class="sxs-lookup"><span data-stu-id="bac1e-151">Run this application and browse for an image containing a face.</span></span> <span data-ttu-id="bac1e-152">Please wait for a few seconds to allow the cloud API to respond.</span><span class="sxs-lookup"><span data-stu-id="bac1e-152">Please wait for a few seconds to allow the cloud API to respond.</span></span> <span data-ttu-id="bac1e-153">After that, you will get a result similar to the image below:</span><span class="sxs-lookup"><span data-stu-id="bac1e-153">After that, you will get a result similar to the image below:</span></span> 

![GettingStartCSharpScreenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/GetStartedCSharp-Detected.PNG)

## <a name="summary"></a> <span data-ttu-id="bac1e-155">Summary</span><span class="sxs-lookup"><span data-stu-id="bac1e-155">Summary</span></span>

<span data-ttu-id="bac1e-156">In this tutorial, you have learned the basic process for using the Face API and created an application to display face marks in images.</span><span class="sxs-lookup"><span data-stu-id="bac1e-156">In this tutorial, you have learned the basic process for using the Face API and created an application to display face marks in images.</span></span> <span data-ttu-id="bac1e-157">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="bac1e-157">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span> 

## <a name="related"></a> <span data-ttu-id="bac1e-158">Related Topics</span><span class="sxs-lookup"><span data-stu-id="bac1e-158">Related Topics</span></span>

- [<span data-ttu-id="bac1e-159">Getting Started with Face API in Java for Android</span><span class="sxs-lookup"><span data-stu-id="bac1e-159">Getting Started with Face API in Java for Android</span></span>](FaceAPIinJavaForAndroidTutorial.md)
- [<span data-ttu-id="bac1e-160">Getting Started with Face API in Python</span><span class="sxs-lookup"><span data-stu-id="bac1e-160">Getting Started with Face API in Python</span></span>](FaceAPIinPythonTutorial.md)







