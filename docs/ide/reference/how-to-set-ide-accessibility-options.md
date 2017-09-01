---
title: 'How to: Set IDE Accessibility Options | Microsoft Docs'
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- accessibility [Visual Studio]
ms.assetid: ddc96c4c-0600-46c1-8267-7dce4c44ad24
author: kempb
ms.author: tglee
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 17defdd0b96ec1c3273fc6b845af844b031a4a17
ms.openlocfilehash: 0bf8db1f5cd1d163edffc7f3673d5b74c40ef8ec
ms.contentlocale: fr-fr
ms.lasthandoff: 08/23/2017

---
# <a name="how-to-set-ide-accessibility-options"></a>How to: Set IDE Accessibility Options
> [!TIP]
> To learn more about recent accessibility updates, see the [Accessibility improvements in Visual Studio 2017 version 15.3](https://blogs.msdn.microsoft.com/visualstudio/2017/08/14/accessibility-improvements-in-visual-studio-2017-version-15-3/) blog post.

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] contains features that make it easier for people who have low vision to read and for people who have limited dexterity to write. These features include changing the size and color of text in editors, changing the size of text and buttons on toolbars, and auto-completion for methods and parameters, to name a few.  

 In addition, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] supports Dvorak keyboard layouts, which make the most frequently typed characters more accessible. You can also customize the default shortcut keys available with [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. For more information, see [Identifying and Customizing Keyboard Shortcuts](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).  

> [!NOTE]
>  The dialog boxes and menu commands you see might differ from those described in Help depending on your active settings or edition. To change your settings, choose **Import and Export Settings** on the **Tools** menu. For more information, see [Personalize the Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md).  

## <a name="editors-dialogs-and-tool-windows"></a>Editors, Dialogs, and Tool Windows  
 By default, dialog boxes and tool windows in [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] use the same font size and colors as the operating system. The color settings for the frame of the IDE, dialog boxes, toolbars, and tool windows are based a color scheme: light or dark. You can change the current color theme in the [General, Environment, Options Dialog Box](../../ide/reference/general-environment-options-dialog-box.md).  

 You can also display pop-up windows in the Code view of the editor. These windows can prompt you with available members on the current object and the parameters to complete a function or statement. These windows can be helpful if you have difficulty typing. However, they interfere with focus in the code editor, which can be problematic for some users. You can turn off these windows by opening the Options dialog box and clearing **Auto list members** and **Parameter information** in the **Text Editor**, **All Languages**, **General** page in the **Options** dialog box. For more information, see [How to: Set General Editor Options](http://msdn.microsoft.com/en-us/704e4a7b-2162-4bed-8a47-f4f6ffec98c2).  

 You can rearrange the windows in the integrated development environment (IDE) to best suit the way you work. You can dock, float, hide, or automatically hide each tool window.  

 For more information about how to change window layouts, see [Customizing window layouts](../../ide/customizing-window-layouts-in-visual-studio.md).  

### <a name="changing-the-size-of-text"></a>Changing the Size of Text  
 You can change the settings for text-based tool windows, such as the **Command** window, **Immediate** window, and **Output** window, in the **Fonts and Colors** pane of the **Environment** options in the **Tools** dialog box. When **[All Text Tool Windows]** is selected in the **Show settings for** drop-down list, the default setting is listed as **Default** in the **Item foreground** and **Item background** drop-down lists. You can also change the settings for how text is displayed in the editor.  

##### <a name="to-change-the-size-of-text-in-text-based-tool-windows-and-editors"></a>To change the size of text in text-based tool windows and editors  

1.  From the **Tools** menu, choose **Options**.  

2.  Choose **Fonts and Colors** on the **Environment** folder.  

3.  Select an option on the **Show settings for** drop-down menu.  

     To change the font size for text in an editor, choose **Text Editor**.  

     To change the font size for text in text-based tool windows, choose **[All Text Tool Windows]**.  

     To change the font size for ToolTip text in an editor, choose **Editor Tooltip**.  

     To change the font size for text in statement completion pop-ups, choose **Statement Completion**.  

4.  From **Display items**, select **Plain Text**.  

5.  In **Font**, select a new font type.  

6.  In **Size**, select a new font size.  

    > [!NOTE]
    >  To reset the text size for text-based tool windows and editors, choose **Use Defaults**.  

7.  Choose **OK**.  

### <a name="changing-the-colors-used-in-the-ide"></a>Changing the Colors used in the IDE  
 You can also choose to change the default colors for text, margin indicators, white space, and code elements in the editor.  

> [!NOTE]
>  To use high contrast colors for all application windows on your operating system, press Left **ALT+**Left **SHIFT+PRINT SCREEN**. If [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] is open, close and reopen [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] to fully implement high contrast colors.  

##### <a name="to-change-the-color-of-items-in-the-editor"></a>To change the color of items in the editor  

1.  From the **Tools** menu, choose **Options**.  

2.  Choose **Fonts and Colors** from the **Environment** folder.  

3.  In **Show settings for**, choose **Text Editor**.  

4.  From **Display items**, select an item whose display you need to change, such as **Plain Text**, **Indicator Margin**, **Visible White Space**, **HTML Attribute Name**, or **XML Attribute**.  

5.  Select display settings from the following options: **Item foreground**, **Item background**, and **Bold**.  

6.  Choose **OK**.  

## <a name="toolbars"></a>Toolbars  
 To improve toolbar usability and accessibility, you can add text to toolbar buttons.  

#### <a name="to-assign-text-to-toolbar-buttons"></a>To assign text to toolbar buttons  

1.  From the **Tools** menu, choose **Customize**.  

2.  In the **Customize** dialog box, select the **Commands** tab.  

3.  Select **Toolbar** and then choose the toolbar name that contains the button you intend to display text for.  

4.  In the list, select the command you intend to change.  

5.  Choose **Modify Selection**.  

6.  Choose **Image and Text**.  

#### <a name="to-modify-the-buttons-displayed-text"></a>To modify the button's displayed text  

1.  Re-select **Modify Selection**.  

2.  Adjacent to In **Name**, insert provide a new caption for the selected button.  

## <a name="see-also"></a>See Also  
 [Accessibility Features of Visual Studio](../../ide/reference/accessibility-features-of-visual-studio.md)   
 [Resources for Designing Accessible Applications](../../ide/reference/resources-for-designing-accessible-applications.md)
