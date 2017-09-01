---
title: 'Walkthrough: Customizing the Text View | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: MT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 3e70313d662d54b48823500a054b5aaa2a9401ae
ms.contentlocale: fr-fr
ms.lasthandoff: 08/30/2017

---
# <a name="walkthrough-customizing-the-text-view"></a>Walkthrough: Customizing the Text View
You can customize a text view by modifying any of the following properties in its editor-format map:  
  
-   Indicator margin  
  
-   Insertion caret  
  
-   Overwrite caret  
  
-   Selected text  
  
-   Inactive selected text (that is, selected text that has lost focus)  
  
-   Visible whitespace  
  
## <a name="prerequisites"></a>Prerequisites  
 Starting in Visual Studio 2015, you do not install the Visual Studio SDK from the download center. It is included as an optional feature in Visual Studio setup. You can also install the VS SDK later on. For more information, see [Installing the Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-mef-project"></a>Creating a MEF Project  
  
1.  Create a C# VSIX project. (In the **New Project** dialog, select **Visual C# / Extensibility**, then **VSIX Project**.) Name the solution `ViewPropertyTest`.  
  
2.  Add an Editor Classifier item template to the project. For more information, see [Creating an Extension with an Editor Item Template](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Delete the existing class files.  
  
## <a name="defining-the-content-type"></a>Defining the Content Type  
  
1.  Add a class file and name it `ViewPropertyModifier`.  
  
2.  Add the following `using` directives:  
  
     [!code-csharp[VSSDKViewPropertyTest#1](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_1.cs)]  [!code-vb[VSSDKViewPropertyTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_1.vb)]  
  
3.  Declare a class named `TestViewCreationListener` that inherits from <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>. Export this class with the following attributes:  
  
    -   <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> to specify the type of content to which this listener applies.  
  
    -   <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> to specify the role of this listener.  
  
     [!code-csharp[VSSDKViewPropertyTest#2](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_2.cs)] [!code-vb[VSSDKViewPropertyTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_2.vb)]  
  
4.  In this class, import the <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>.  
  
     [!code-csharp[VSSDKViewPropertyTest#3](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_3.cs)]  [!code-vb[VSSDKViewPropertyTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_3.vb)]  
  
## <a name="changing-the-view-properties"></a>Changing the View Properties  
  
1.  Implement the <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> method so that the view properties are changed when the view is opened. To make the change, first find the <xref:System.Windows.ResourceDictionary> that corresponds to the aspect of the view you want to find. Then change the appropriate property in the resource dictionary and set the properties. Batch the calls to the <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A> method by calling the <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> method before you set the properties and then the <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> after you set the properties.  
  
     [!code-csharp[VSSDKViewPropertyTest#4](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_4.cs)]  [!code-vb[VSSDKViewPropertyTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_4.vb)]  
  
## <a name="building-and-testing-the-code"></a>Building and Testing the Code  
  
1.  Build the solution.  
  
     When you run this project in the debugger, a second instance of Visual Studio is instantiated.  
  
2.  Create a text file and type some text.  
  
    -   The insertion caret should be magenta and the overwrite caret should be turquoise.  
  
    -   The indicator margin (to the left of the text view) should be light green.  
  
3.  Select the text you just typed. The color of the selected text should be light pink.  
  
4.  While the text is selected, click anywhere outside the text window. The color of the selected text should be dark pink.  
  
5.  Turn on visible whitespace. (On the **Edit** menu, point to **Advanced** and then click **View White Space**). Type some tabs in the text. Red arrows that represent the tabs should be displayed.  
  
## <a name="see-also"></a>See Also  
 [Language Service and Editor Extension Points](../extensibility/language-service-and-editor-extension-points.md)