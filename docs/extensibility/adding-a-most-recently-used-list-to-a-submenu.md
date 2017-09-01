---
title: Adding a Most Recently Used List to a Submenu | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
caps.latest.revision: 46
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: b494bec6dda9e6252243005ef817798f65d0a0be
ms.contentlocale: fr-fr
ms.lasthandoff: 08/28/2017

---
# <a name="adding-a-most-recently-used-list-to-a-submenu"></a>Adding a Most Recently Used List to a Submenu
This walkthrough builds on the demonstrations in [Adding a Submenu to a Menu](../extensibility/adding-a-submenu-to-a-menu.md), and shows how to add a dynamic list to a submenu. The dynamic list forms the basis for creating a Most Recently Used (MRU) list.  
  
 A dynamic menu list starts with a placeholder on a menu. Every time the menu is shown, the Visual Studio integrated development environment (IDE) asks the VSPackage for all commands that should be shown at the placeholder. A dynamic list can occur anywhere on a menu. However, dynamic lists are typically stored and displayed by themselves on submenus or at the bottoms of menus. By using these design patterns, you enable the dynamic list of commands to expand and contract without affecting the position of other commands on the menu. In this walkthrough, the dynamic MRU list is displayed at the bottom of an existing submenu, separated from the rest of the submenu by a line.  
  
 Technically, a dynamic list can also be applied to a toolbar. However, we discourage that usage because a toolbar should remain unchanged unless the user takes specific steps to change it.  
  
 This walkthrough creates an MRU list of four items that change their order every time that one of them is selected (the selected item moves to the top of the list).  
  
 For more information about menus and .vsct files, see [Commands, Menus, and Toolbars](../extensibility/internals/commands-menus-and-toolbars.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 To follow this walkthrough, you must install the Visual Studio SDK. For more information, see [Visual Studio SDK](../extensibility/visual-studio-sdk.md).  
  
## <a name="creating-an-extension"></a>Creating an Extension  
  
-   Follow the procedures in [Adding a Submenu to a Menu](../extensibility/adding-a-submenu-to-a-menu.md) to create the submenu that is modified in the following procedures.  
  
 The procedures in this walkthrough assume that the name of the VSPackage is `TopLevelMenu`, which is the name that is used in [Adding a Menu to the Visual Studio Menu Bar](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md).  
  
## <a name="creating-a-dynamic-item-list-command"></a>Creating a Dynamic Item List Command  
  
1.  Open TestCommandPackage.vsct.  
  
2.  In the `Symbols` section, in the `GuidSymbol` node named guidTestCommandPackageCmdSet, add the symbol for the `MRUListGroup` group and the `cmdidMRUList` command, as follows.  
  
    ```csharp  
    <IDSymbol name="MRUListGroup" value="0x1200"/>  
    <IDSymbol name="cmdidMRUList" value="0x0200"/>  
    ```  
  
3.  In the `Groups` section, add the declared group after the existing group entries.  
  
    ```cpp  
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"   
           priority="0x0100">  
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>  
    </Group>  
  
    ```  
  
4.  In the `Buttons` section, add a node to represent the newly declared command, after the existing button entries.  
  
    ```csharp  
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"  
        type="Button" priority="0x0100">  
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />  
        <CommandFlag>DynamicItemStart</CommandFlag>  
        <Strings>  
            <CommandName>cmdidMRUList</CommandName>  
            <ButtonText>MRU Placeholder</ButtonText>  
                </Strings>  
    </Button>  
    ```  
  
     The `DynamicItemStart` flag enables the command to be generated dynamically.  
  
5.  Build the project and start debugging to test the display of the new command.  
  
     On the **TestMenu** menu, click the new submenu, **Sub Menu**, to display the new command, **MRU Placeholder**. After a dynamic MRU list of commands is implemented in the next procedure, this command label will be replaced by that list every time that the submenu is opened.  
  
## <a name="filling-the-mru-list"></a>Filling the MRU List  
  
1.  In TestCommandPackageGuids.cs, add the following lines after the existing command IDs in the `TestCommandPackageGuids` class definition.  
  
    ```csharp  
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file  
    public const uint cmdidMRUList = 0x200;  
    ```  
  
2.  In TestCommand.cs add the following using statement.  
  
    ```csharp  
    using System.Collections;  
    ```  
  
3.  Add the following code in the TestCommand constructor after the last AddCommand call. The `InitMRUMenu` will be defined later  
  
    ```csharp  
    this.InitMRUMenu(commandService);  
    ```  
  
4.  Add the following code in the TestCommand class. This code initializes the list of strings that represent the items to be shown on the MRU list.  
  
    ```csharp  
    private int numMRUItems = 4;  
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;  
    private ArrayList mruList;  
  
    private void InitializeMRUList()  
    {  
        if (null == this.mruList)  
        {  
            this.mruList = new ArrayList();  
            if (null != this.mruList)  
            {  
                for (int i = 0; i < this.numMRUItems; i++)  
                {  
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,  
                        "Item {0}", i + 1));  
                }  
            }  
        }  
    }  
    ```  
  
5.  After the `InitializeMRUList` method, add the `InitMRUMenu` method. This initializes the MRU list menu commands.  
  
    ```csharp  
    private void InitMRUMenu(OleMenuCommandService mcs)  
    {  
        InitializeMRUList();  
        for (int i = 0; i < this.numMRUItems; i++)  
        {  
            var cmdID = new CommandID(  
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);  
            var mc = new OleMenuCommand(  
                new EventHandler(OnMRUExec), cmdID);  
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);  
            mcs.AddCommand(mc);  
        }  
    }  
    ```  
  
     You must create a menu command object for every possible item in the MRU list. The IDE calls the `OnMRUQueryStatus` method for each item in the MRU list until there are no more items. In managed code, the only way for the IDE to know that there are no more items is to create all possible items first. If you want, you can mark additional items as not visible at first by using `mc.Visible = false;` after the menu command is created. These items can then be made visible later by using `mc.Visible = true;` in the `OnMRUQueryStatus` method.  
  
6.  After the `InitMRUMenu` method, add the following `OnMRUQueryStatus` method. This is the handler that sets the text for each MRU item.  
  
    ```csharp  
    private void OnMRUQueryStatus(object sender, EventArgs e)  
    {  
        OleMenuCommand menuCommand = sender as OleMenuCommand;  
        if (null != menuCommand)  
        {  
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;  
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)  
            {  
                menuCommand.Text = this.mruList[MRUItemIndex] as string;  
            }  
        }  
    }  
    ```  
  
7.  After the `OnMRUQueryStatus` method, add the following `OnMRUExec` method. This is the handler for selecting an MRU item. This method moves the selected item to the top of the list and then displays the selected item in a message box.  
  
    ```csharp  
    private void OnMRUExec(object sender, EventArgs e)  
    {  
        var menuCommand = sender as OleMenuCommand;  
        if (null != menuCommand)  
        {  
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;  
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)  
            {  
                string selection = this.mruList[MRUItemIndex] as string;  
                for (int i = MRUItemIndex; i > 0; i--)  
                {  
                    this.mruList[i] = this.mruList[i - 1];  
                }  
                this.mruList[0] = selection;  
                System.Windows.Forms.MessageBox.Show(  
                    string.Format(CultureInfo.CurrentCulture,  
                                  "Selected {0}", selection));  
            }  
        }  
    }  
  
    ```  
  
## <a name="testing-the-mru-list"></a>Testing the MRU List  
  
#### <a name="to-test-the-mru-menu-list"></a>To test the MRU menu list  
  
1.  Build the project and start debugging  
  
2.  On the **TestMenu** menu, click **Invoke TestCommand**. Doing this displays a message box that indicates that the command was selected.  
  
    > [!NOTE]
    >  This step is required to force the VSPackage to load and correctly display the MRU list. If you skip this step, the MRU list is not displayed.  
  
3.  On the **Test Menu** menu, click **Sub Menu**. A list of four items is displayed at the end of the submenu, below a separator. When you click **Item 3**, a message box should appear and display the text, "Selected Item 3". (If the list of four items is not displayed, ensure that you have followed the instructions in the earlier step.)  
  
4.  Open the submenu again. Notice that **Item 3** is now at the top of the list and the other items have been pushed down one position. Click **Item 3** again and notice that the message box still displays "Selected Item 3", which indicates that the text has correctly moved to the new position together with the command label.  
  
## <a name="see-also"></a>See Also  
 [Dynamically Adding Menu Items](../extensibility/dynamically-adding-menu-items.md)