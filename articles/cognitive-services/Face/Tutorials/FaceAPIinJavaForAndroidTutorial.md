---
title: Face API Java for Android tutorial | Microsoft Docs
description: Create a simple Android app that uses the Cognitive Services Face API to detect and frame human faces in an image.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 02/24/2017
ms.author: anroth
ms.openlocfilehash: ff1013430e959368e7e5330eda15db1d16480738
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540898"
---
# <a name="getting-started-with-face-api-in-java-for-android-tutorial"></a><span data-ttu-id="7b4ae-103">Getting Started with Face API in Java for Android Tutorial</span><span class="sxs-lookup"><span data-stu-id="7b4ae-103">Getting Started with Face API in Java for Android Tutorial</span></span>

<span data-ttu-id="7b4ae-104">In this tutorial, you will learn to create and develop a simple Android application that invokes the Face API to detect human faces in an image.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-104">In this tutorial, you will learn to create and develop a simple Android application that invokes the Face API to detect human faces in an image.</span></span> <span data-ttu-id="7b4ae-105">The application shows the result by framing the faces that it detects.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-105">The application shows the result by framing the faces that it detects.</span></span>     

![GettingStartedAndroid](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/android_getstarted2.1.PNG)

## <a name="preparation"></a> <span data-ttu-id="7b4ae-107">Preparation</span><span class="sxs-lookup"><span data-stu-id="7b4ae-107">Preparation</span></span>

<span data-ttu-id="7b4ae-108">To use the tutorial, you will need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-108">To use the tutorial, you will need the following prerequisites:</span></span>

- <span data-ttu-id="7b4ae-109">Android Studio and SDK installed</span><span class="sxs-lookup"><span data-stu-id="7b4ae-109">Android Studio and SDK installed</span></span>
- <span data-ttu-id="7b4ae-110">Android device (optional for testing)</span><span class="sxs-lookup"><span data-stu-id="7b4ae-110">Android device (optional for testing)</span></span> 

## <a name="step1"></a><span data-ttu-id="7b4ae-111">Step 1: Subscribe for Face API and get your subscription key</span><span class="sxs-lookup"><span data-stu-id="7b4ae-111">Step 1: Subscribe for Face API and get your subscription key</span></span>

<span data-ttu-id="7b4ae-112">Before using any Face API, you must sign up to subscribe to Face API in the Microsoft Cognitive Services (formerly Project Oxford) portal.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-112">Before using any Face API, you must sign up to subscribe to Face API in the Microsoft Cognitive Services (formerly Project Oxford) portal.</span></span> <span data-ttu-id="7b4ae-113">See [subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="7b4ae-113">See [subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="7b4ae-114">Both primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-114">Both primary and secondary key can be used in this tutorial.</span></span>

## <a name="step2"></a><span data-ttu-id="7b4ae-115">Step 2: Create the application framework</span><span class="sxs-lookup"><span data-stu-id="7b4ae-115">Step 2: Create the application framework</span></span>

<span data-ttu-id="7b4ae-116">In this step you will create an Android application project to implement the basic UI for picking up and displaying an image.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-116">In this step you will create an Android application project to implement the basic UI for picking up and displaying an image.</span></span> <span data-ttu-id="7b4ae-117">Simply follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-117">Simply follow the instructions below:</span></span> 

1. <span data-ttu-id="7b4ae-118">Open Android Studio.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-118">Open Android Studio.</span></span>
2. <span data-ttu-id="7b4ae-119">From the File menu, click New Project…</span><span class="sxs-lookup"><span data-stu-id="7b4ae-119">From the File menu, click New Project…</span></span>
3. <span data-ttu-id="7b4ae-120">Name the application MyFirstApp, and then click Next.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-120">Name the application MyFirstApp, and then click Next.</span></span> 

    ![GettingStartAndroidNewProject](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/AndroidNewProject.png)

4. <span data-ttu-id="7b4ae-122">Choose target platform as required, and then click Next.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-122">Choose target platform as required, and then click Next.</span></span> 

    ![GettingStartAndroidNewProject2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/AndroidNewProject2.png)

5. <span data-ttu-id="7b4ae-124">Select "Basic Activity" and then click Next.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-124">Select "Basic Activity" and then click Next.</span></span>
6. <span data-ttu-id="7b4ae-125">Name the activity as follows, and then click Finish.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-125">Name the activity as follows, and then click Finish.</span></span> 

    ![GettingStartAndroidNewProject4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/AndroidNewProject4.png)

7. <span data-ttu-id="7b4ae-127">Open activity_main.xml, you should see the Layout Editor of this activity.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-127">Open activity_main.xml, you should see the Layout Editor of this activity.</span></span>
8. <span data-ttu-id="7b4ae-128">View Text source file and then edit the activity layout as follows:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-128">View Text source file and then edit the activity layout as follows:</span></span>           

    ```xml
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
        android:paddingRight="@dimen/activity_horizontal_margin"
        android:paddingTop="@dimen/activity_vertical_margin"
        android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
     
        <ImageView
            android:layout_width="match_parent"
            android:layout_height="fill_parent"
            android:id="@+id/imageView1"
            android:layout_above="@+id/button1" />
    
        <Button
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Browse"
            android:id="@+id/button1"
            android:layout_alignParentBottom="true" />
    </RelativeLayout>
    ```  

9. <span data-ttu-id="7b4ae-129">Open MainActivity.java and insert the following import directives at the beginning of the file:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-129">Open MainActivity.java and insert the following import directives at the beginning of the file:</span></span>           

        import java.io.*; 
        import android.app.*; 
        import android.content.*; 
        import android.net.*; 
        import android.os.*; 
        import android.view.*; 
        import android.graphics.*; 
        import android.widget.*; 
        import android.provider.*;
      
    <span data-ttu-id="7b4ae-130">Secondly, Modify the onCreate method of the MainActivity class for the 'Browse' button logic:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-130">Secondly, Modify the onCreate method of the MainActivity class for the 'Browse' button logic:</span></span>  

        private final int PICK_IMAGE = 1;
        private ProgressDialog detectionProgressDialog;
         
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            Button button1 = (Button)findViewById(R.id.button1);
            button1.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    Intent gallIntent = new Intent(Intent.ACTION_GET_CONTENT);
                    gallIntent.setType("image/*");
                    startActivityForResult(Intent.createChooser(gallIntent, "Select Picture"), PICK_IMAGE);
                }
        });
         
        detectionProgressDialog = new ProgressDialog(this);
        }
        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            super.onActivityResult(requestCode, resultCode, data);
            if (requestCode == PICK_IMAGE && resultCode == RESULT_OK && data != null && data.getData() != null) {
                Uri uri = data.getData();
                try {
                    Bitmap bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), uri);
                    ImageView imageView = (ImageView) findViewById(R.id.imageView1);
                    imageView.setImageBitmap(bitmap);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }  

<span data-ttu-id="7b4ae-131">Now your app can browse for a photo from the gallery and display it in the window similar to the image below:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-131">Now your app can browse for a photo from the gallery and display it in the window similar to the image below:</span></span>

![GettingStartAndroidUI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/android_getstarted1.1.PNG)

## <a name="step3"></a><span data-ttu-id="7b4ae-133">Step 3: Configure the Face API client library</span><span class="sxs-lookup"><span data-stu-id="7b4ae-133">Step 3: Configure the Face API client library</span></span>

<span data-ttu-id="7b4ae-134">The Face API is a cloud API which you can invoke using HTTPS requests.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-134">The Face API is a cloud API which you can invoke using HTTPS requests.</span></span> <span data-ttu-id="7b4ae-135">For a more convenient way of using the Face API in .NET platform applications, a client library is also provided to encapsulate the web requests.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-135">For a more convenient way of using the Face API in .NET platform applications, a client library is also provided to encapsulate the web requests.</span></span> <span data-ttu-id="7b4ae-136">In this example, we use the client library to simplify our work.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-136">In this example, we use the client library to simplify our work.</span></span> 

<span data-ttu-id="7b4ae-137">Follow the instructions below to configure the client library:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-137">Follow the instructions below to configure the client library:</span></span> 

1. <span data-ttu-id="7b4ae-138">Locate the top-level build.gradle file of your project from the Project panel shown in the exapmle.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-138">Locate the top-level build.gradle file of your project from the Project panel shown in the exapmle.</span></span> <span data-ttu-id="7b4ae-139">Note that there are several other build.gradle files in your project tree, and you need to open the top-level build.gradle file at first.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-139">Note that there are several other build.gradle files in your project tree, and you need to open the top-level build.gradle file at first.</span></span>         
2. <span data-ttu-id="7b4ae-140">Add mavenCentral() to your projects' repositories.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-140">Add mavenCentral() to your projects' repositories.</span></span> <span data-ttu-id="7b4ae-141">You can also use jcenter(), which is the default repository of Android Studio, since jcenter() is a superset of mavenCentral().</span><span class="sxs-lookup"><span data-stu-id="7b4ae-141">You can also use jcenter(), which is the default repository of Android Studio, since jcenter() is a superset of mavenCentral().</span></span>  

        allprojects {
            repositories {
                ...
                mavenCentral()
            }
        }

3. <span data-ttu-id="7b4ae-142">Open the build.gradle file in your 'app' project.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-142">Open the build.gradle file in your 'app' project.</span></span>
4. <span data-ttu-id="7b4ae-143">Add a dependency for our client library stored in the Maven Central Repository:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-143">Add a dependency for our client library stored in the Maven Central Repository:</span></span>

        dependencies {  
            ...  
            compile 'com.microsoft.projectoxford:face:1.0.0'  
        }  

5. <span data-ttu-id="7b4ae-144">Open MainActivity.java in your 'app' project and insert the following import directives:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-144">Open MainActivity.java in your 'app' project and insert the following import directives:</span></span> 
    
        import com.microsoft.projectoxford.face.\*;  
        import com.microsoft.projectoxford.face.contract.\*;  
    
   <span data-ttu-id="7b4ae-145">And then insert the following code in the MainActivity class:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-145">And then insert the following code in the MainActivity class:</span></span>

        private FaceServiceClient faceServiceClient =  
                    new FaceServiceRestClient("your subscription key");  

   <span data-ttu-id="7b4ae-146">Replace the string above with the subscription key you obtained in step 1.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-146">Replace the string above with the subscription key you obtained in step 1.</span></span>  
6. <span data-ttu-id="7b4ae-147">Open the file called AndroidManifest.xml in your 'app' project (in the app/src/main directory).</span><span class="sxs-lookup"><span data-stu-id="7b4ae-147">Open the file called AndroidManifest.xml in your 'app' project (in the app/src/main directory).</span></span> <span data-ttu-id="7b4ae-148">Insert the following element into the manifest element:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-148">Insert the following element into the manifest element:</span></span>  

        <uses-permission android:name="android.permission.INTERNET" />  

7. <span data-ttu-id="7b4ae-149">Now you are ready to call the Face API from your application.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-149">Now you are ready to call the Face API from your application.</span></span> 

## <a name="step4"></a><span data-ttu-id="7b4ae-150">Step 4: Upload images to detect faces</span><span class="sxs-lookup"><span data-stu-id="7b4ae-150">Step 4: Upload images to detect faces</span></span>

<span data-ttu-id="7b4ae-151">The most straightforward way to detect faces is by calling the [Face – Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API by uploading the image file directly.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-151">The most straightforward way to detect faces is by calling the [Face – Detect](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) API by uploading the image file directly.</span></span> <span data-ttu-id="7b4ae-152">When using the client library, this can be done by using an asynchronous method DetectAsync of FaceServiceClient.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-152">When using the client library, this can be done by using an asynchronous method DetectAsync of FaceServiceClient.</span></span> <span data-ttu-id="7b4ae-153">Each returned face contains a rectangle to indicate its location, combined with a series of optional face attributes.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-153">Each returned face contains a rectangle to indicate its location, combined with a series of optional face attributes.</span></span> <span data-ttu-id="7b4ae-154">In this example, we only need to retrieve the face location.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-154">In this example, we only need to retrieve the face location.</span></span> <span data-ttu-id="7b4ae-155">Here we need to insert a method into the MainActivity class for face detection:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-155">Here we need to insert a method into the MainActivity class for face detection:</span></span> 

    // Detect faces by uploading face images
    // Frame faces after detection
    
    private void detectAndFrame(final Bitmap imageBitmap)
    {
        ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
        imageBitmap.compress(Bitmap.CompressFormat.JPEG, 100, outputStream);
        ByteArrayInputStream inputStream = 
            new ByteArrayInputStream(outputStream.toByteArray());
        AsyncTask<InputStream, String, Face[]> detectTask =
            new AsyncTask<InputStream, String, Face[]>() {
                @Override
                protected Face[] doInBackground(InputStream... params) {
                    try {
                        publishProgress("Detecting...");
                        Face[] result = faceServiceClient.detect(
                                params[0], 
                                true,         // returnFaceId
                                false,        // returnFaceLandmarks
                                null           // returnFaceAttributes: a string like "age, gender"
                        );
                        if (result == null)
                        {
                            publishProgress("Detection Finished. Nothing detected");
                            return null;
                        }
                        publishProgress(
                                String.format("Detection Finished. %d face(s) detected",
                                        result.length));
                        return result;
                    } catch (Exception e) {
                        publishProgress("Detection failed");
                        return null;
                    }
                }
                @Override
                protected void onPreExecute() {
                    //TODO: show progress dialog
                }
                @Override
                protected void onProgressUpdate(String... progress) {
                    //TODO: update progress
                }
                @Override
                protected void onPostExecute(Face[] result) {
                    //TODO: update face frames
                }
            };
        detectTask.execute(inputStream);
    }

## <a name="step5"></a><span data-ttu-id="7b4ae-156">Step 5: Mark faces in the image</span><span class="sxs-lookup"><span data-stu-id="7b4ae-156">Step 5: Mark faces in the image</span></span>

<span data-ttu-id="7b4ae-157">In this last step, we combine all the above steps together and mark the detected faces with frames in the image.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-157">In this last step, we combine all the above steps together and mark the detected faces with frames in the image.</span></span> <span data-ttu-id="7b4ae-158">First, open MainActivity.java and insert a helper method in MainActivity.java to draw rectangles:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-158">First, open MainActivity.java and insert a helper method in MainActivity.java to draw rectangles:</span></span> 

    private static Bitmap drawFaceRectanglesOnBitmap(Bitmap originalBitmap, Face[] faces) {
        Bitmap bitmap = originalBitmap.copy(Bitmap.Config.ARGB_8888, true);
        Canvas canvas = new Canvas(bitmap);
        Paint paint = new Paint();
        paint.setAntiAlias(true);
        paint.setStyle(Paint.Style.STROKE);
        paint.setColor(Color.RED);
        int stokeWidth = 2;
        paint.setStrokeWidth(stokeWidth);
        if (faces != null) {
            for (Face face : faces) {
                FaceRectangle faceRectangle = face.faceRectangle;
                canvas.drawRect(
                        faceRectangle.left,
                        faceRectangle.top,
                        faceRectangle.left + faceRectangle.width,
                        faceRectangle.top + faceRectangle.height,
                        paint);
            }
        }
        return bitmap;
    }

<span data-ttu-id="7b4ae-159">Now finish the TODO parts in the detectAndFrame method in order to frame faces and report status.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-159">Now finish the TODO parts in the detectAndFrame method in order to frame faces and report status.</span></span>   

    @Override
    protected void onPreExecute() {
        
        detectionProgressDialog.show();
    }
    @Override
    protected void onProgressUpdate(String... progress) {
        
        detectionProgressDialog.setMessage(progress[0]);
    }
    @Override
    protected void onPostExecute(Face[] result) {
        
        detectionProgressDialog.dismiss();
        if (result == null) return;
        ImageView imageView = (ImageView)findViewById(R.id.imageView1);
        imageView.setImageBitmap(drawFaceRectanglesOnBitmap(imageBitmap, result));
        imageBitmap.recycle();
    }
 
<span data-ttu-id="7b4ae-160">Finally, add a call to the detectAndFrame method from the onActivityResult method, as shown below.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-160">Finally, add a call to the detectAndFrame method from the onActivityResult method, as shown below.</span></span> <span data-ttu-id="7b4ae-161">(Note that the asterisks are only intended to highlight the new addition.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-161">(Note that the asterisks are only intended to highlight the new addition.</span></span> <span data-ttu-id="7b4ae-162">You must remove them before attempting to build the code.)</span><span class="sxs-lookup"><span data-stu-id="7b4ae-162">You must remove them before attempting to build the code.)</span></span>  

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == PICK_IMAGE && resultCode == RESULT_OK && data != null && data.getData() != null) {
            Uri uri = data.getData();
            try {
                Bitmap bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), uri);
                ImageView imageView = (ImageView) findViewById(R.id.imageView1);
                imageView.setImageBitmap(bitmap);
     
                **detectAndFrame(bitmap);**
     
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

<span data-ttu-id="7b4ae-163">Run this application and browse for an image containing a face.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-163">Run this application and browse for an image containing a face.</span></span> <span data-ttu-id="7b4ae-164">Please wait for a few seconds to allow the cloud API to respond.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-164">Please wait for a few seconds to allow the cloud API to respond.</span></span> <span data-ttu-id="7b4ae-165">After that, you will get a result similar to the image below:</span><span class="sxs-lookup"><span data-stu-id="7b4ae-165">After that, you will get a result similar to the image below:</span></span> 

![GettingStartAndroid](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Face/Images/android_getstarted2.1.PNG)

## <a name="summary"></a> <span data-ttu-id="7b4ae-167">Summary</span><span class="sxs-lookup"><span data-stu-id="7b4ae-167">Summary</span></span>

<span data-ttu-id="7b4ae-168">In this tutorial, you learned the basic process for using the Face API and created an application to display face marks in images.</span><span class="sxs-lookup"><span data-stu-id="7b4ae-168">In this tutorial, you learned the basic process for using the Face API and created an application to display face marks in images.</span></span> <span data-ttu-id="7b4ae-169">For more information on the Face API, refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="7b4ae-169">For more information on the Face API, refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span> 

## <a name="related"></a> <span data-ttu-id="7b4ae-170">Related Tutorials</span><span class="sxs-lookup"><span data-stu-id="7b4ae-170">Related Tutorials</span></span>

- [<span data-ttu-id="7b4ae-171">Getting Started with Face API in CSharp Tutorial</span><span class="sxs-lookup"><span data-stu-id="7b4ae-171">Getting Started with Face API in CSharp Tutorial</span></span>](FaceAPIinCSharpTutorial.md)
- [<span data-ttu-id="7b4ae-172">Getting Started with Face API in Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="7b4ae-172">Getting Started with Face API in Python Tutorial</span></span>](FaceAPIinPythonTutorial.md)






