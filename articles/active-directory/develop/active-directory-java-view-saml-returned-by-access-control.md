---
title: View SAML Returned by the Access Control Service (Java)
description: Learn how to view SAML returned by the Access Control Service in Java applications hosted on Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: b81cbe69a45ddab5e0673e27ed0d3bab807a69a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549382"
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="9cced-103">How to view SAML returned by the Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="9cced-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="9cced-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="9cced-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="9cced-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span><span class="sxs-lookup"><span data-stu-id="9cced-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="9cced-106">The completed application will look similar to the following.</span><span class="sxs-lookup"><span data-stu-id="9cced-106">The completed application will look similar to the following.</span></span>

![Example SAML output][saml_output]

<span data-ttu-id="9cced-108">For more information on ACS, see the [Next steps](#next_steps) section.</span><span class="sxs-lookup"><span data-stu-id="9cced-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="9cced-109">The Azure Access Services Control Filter is a community technology preview.</span><span class="sxs-lookup"><span data-stu-id="9cced-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="9cced-110">As pre-release software, it is not formally supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cced-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9cced-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9cced-111">Prerequisites</span></span>
<span data-ttu-id="9cced-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9cced-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="9cced-113">Add the JspWriter library to your build path and deployment assembly</span><span class="sxs-lookup"><span data-stu-id="9cced-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="9cced-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span><span class="sxs-lookup"><span data-stu-id="9cced-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="9cced-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span><span class="sxs-lookup"><span data-stu-id="9cced-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="9cced-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span><span class="sxs-lookup"><span data-stu-id="9cced-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="9cced-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="9cced-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="9cced-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span><span class="sxs-lookup"><span data-stu-id="9cced-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="9cced-119">In the **Web Deployment Assembly** dialog, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9cced-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="9cced-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9cced-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="9cced-121">Select the appropriate library and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9cced-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="9cced-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span><span class="sxs-lookup"><span data-stu-id="9cced-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="9cced-123">Modify the JSP file to display SAML</span><span class="sxs-lookup"><span data-stu-id="9cced-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="9cced-124">Modify **index.jsp** to use the following code.</span><span class="sxs-lookup"><span data-stu-id="9cced-124">Modify **index.jsp** to use the following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate the child nodes of the doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-the-application"></a><span data-ttu-id="9cced-125">Run the application</span><span class="sxs-lookup"><span data-stu-id="9cced-125">Run the application</span></span>
1. <span data-ttu-id="9cced-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9cced-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="9cced-127">Launch a browser and open your web application.</span><span class="sxs-lookup"><span data-stu-id="9cced-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="9cced-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span><span class="sxs-lookup"><span data-stu-id="9cced-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cced-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="9cced-129">Next steps</span></span>
<span data-ttu-id="9cced-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="9cced-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png

