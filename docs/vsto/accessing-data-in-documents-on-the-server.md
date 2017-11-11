---
title: Accessing Data in Documents on the Server | Microsoft Docs
ms.custom: 
ms.date: 02/02/2017
ms.prod: visual-studio-dev14
ms.reviewer: 
ms.suite: 
ms.technology:
- office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
ms.assetid: 14a42e96-ed2f-48a1-a0c0-e19f9eba4956
caps.latest.revision: 32
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 2e40f5a2c4daa058dfdff06354904dc3a8a0a4fe
ms.contentlocale: pt-br
ms.lasthandoff: 08/30/2017

---
# <a name="accessing-data-in-documents-on-the-server"></a>Accessing Data in Documents on the Server
  You can program against the data in a document-level customization without having to use the object model of Microsoft Office Word or Microsoft Office Excel. This means that you can access data that is contained in a document on a server that does not have Word or Excel installed. For example, code on a server (for instance, in an [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] page) can customize the data in a document and send the customized document to an end user. When the end user opens the document, data binding code in the solution assembly binds the customized data into the document. This is possible because the data in the document is separated from the user interface. For more information, see [Cached Data in Document-Level Customizations](../vsto/cached-data-in-document-level-customizations.md).  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="caching-data-for-use-on-a-server"></a>Caching Data for Use on a Server  
 To cache a data object in a document, mark it with the <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> attribute at design time, or use the `StartCaching` method of a host item at run time. When you cache a data object in a document, the [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] serializes the object into an XML string that is stored in the document. Objects must meet certain requirements to be eligible for caching. For more information, see [Caching Data](../vsto/caching-data.md).  
  
 Server-side code can manipulate any data objects in the data cache. Controls that are bound to cached data instances are synchronized with the user interface, so that any server-side changes that are made to the data show up automatically when the document is opened on the client.  
  
## <a name="accessing-data-in-the-cache"></a>Accessing Data in the Cache  
 You can access data in the cache from applications outside of Office, for example from a console application, a Windows Forms application, or a Web page. The application that accesses the cached data must have full trust; a Web application that has partial trust cannot insert, retrieve, or change data that is cached in an Office document.  
  
 The data cache is accessible through a hierarchy of collections that are exposed by the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> property of the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> class:  
  
-   The <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> property returns a <xref:Microsoft.VisualStudio.Tools.Applications.CachedData>, which contains all of the cached data in a document-level customization.  
  
-   Each <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> contains one or more <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> objects. A <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> contains all of the cached data objects that are defined within a single class.  
  
-   Each <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> contains one or more <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> objects. A <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> represents a single cached data object.  
  
 The following code example demonstrates how to access a cached string in the `Sheet1` class of an Excel workbook project. This example is part of a larger example that is provided for the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> method.  
  
 [!code-csharp[Trin_ServerDocument#12](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#12)] [!code-vb[Trin_ServerDocument#12](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#12)]  
  
## <a name="modifying-data-in-the-cache"></a>Modifying Data in the Cache  
 To modify a cached data object, you typically perform the following steps:  
  
1.  Deserialize the XML representation of the cached object into a new instance of the object. You can access the XML by using the <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> property of the <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> that represents the cached data object.  
  
2.  Make the changes to this copy.  
  
3.  Serialize the changed object back into the data cache by using one of the following options:  
  
    -   If you want to automatically serialize the changes, use the <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> method. This method uses the **DiffGram** format for serializing <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, and typed dataset objects in the data cache. The **DiffGram** format ensures that changes to the data cache in an offline document are sent to the server correctly.  
  
    -   If you want to perform your own serialization for changes to cached data, you can write directly to the <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> property. Specify the **DiffGram** format if you use a <xref:System.Data.Common.DataAdapter> to update a database with changes made to data in a <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, or typed dataset. Otherwise, the <xref:System.Data.Common.DataAdapter> will update the database by adding new rows instead of modifying existing rows.  
  
### <a name="modifying-data-without-deserializing-the-current-value"></a>Modifying Data Without Deserializing the Current Value  
 In some cases, you might want to modify the value of the cached object without first deserializing the current value. For example, you can do this if you are changing the value of an object that has a simple type, such as a string or integer, or if you are initializing a cached <xref:System.Data.DataSet> in a document on a server. In these cases, you can use the <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> method without first deserializing the current value of the cached object.  
  
 The following code example demonstrates how to change the value of a cached string in the `Sheet1` class of an Excel workbook project. This example is part of a larger example that is provided for the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> method.  
  
 [!code-csharp[Trin_ServerDocument#11](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#11)] [!code-vb[Trin_ServerDocument#11](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#11)]  
  
### <a name="modifying-null-values-in-the-data-cache"></a>Modifying Null Values in the Data Cache  
 The data cache does not store objects that have the value **null** when the document is saved and closed. This limitation has several consequences when you modify cached data:  
  
-   If you set any object in the data cache to the value **null**, all of the objects in the data cache will be automatically set to **null** when the document is opened, and the entire data cache will be cleared when the document is saved and closed. That is, all of the cached objects will be removed from the data cache, and the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> collection will be empty.  
  
-   If you build a solution with **null** objects in the data cache and you want to initialize these objects by using the <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> class before the document is opened for the first time, you must ensure that you initialize all of the objects in the data cache. If you initialize only some of the objects, all of the objects will be set to **null** when the document is opened, and the entire data cache will be cleared when the document is saved and closed.  
  
## <a name="accessing-typed-datasets-in-the-cache"></a>Accessing Typed Datasets in the Cache  
 If you want to access the data in a typed dataset both from an Office solution and from an application outside of Office, such as a Windows Forms application or an [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] project, you must define the typed dataset in a separate assembly that is referenced in both projects. If you add the typed dataset to each project by using the **Data Source Configuration Wizard** or the **Dataset Designer**, the .NET Framework will treat the typed datasets in the two projects as different types. For more information about creating typed datasets, see [Create and configure datasets in Visual Studio](/visualstudio/data-tools/create-and-configure-datasets-in-visual-studio).  
  
## <a name="see-also"></a>See Also  
 [Accessing Data in Documents on the Server](../vsto/accessing-data-in-documents-on-the-server.md)   
 [Cached Data in Document-Level Customizations](../vsto/cached-data-in-document-level-customizations.md)  
  
  