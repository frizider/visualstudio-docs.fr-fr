---
title: "Ouverture d’une fenêtre outil dynamique | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
caps.latest.revision: "21"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 588badc75a604df65949c99fa16f84ad4e9c9175
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="opening-a-dynamic-tool-window"></a>Ouverture d’une fenêtre outil dynamique
Fenêtres Outil sont généralement ouvert à partir d’une commande dans un menu ou un raccourci clavier équivalent. Dans certains cas, toutefois, vous devrez peut-être une fenêtre outil qui s’ouvre chaque fois qu’un contexte de l’interface utilisateur spécifique s’applique et se ferme lorsque le contexte de l’interface utilisateur ne s’applique plus. Les fenêtres Outil comme celles-ci sont appelées *dynamique* ou *visibles automatiquement*.  
  
> [!NOTE]
>  Pour obtenir la liste des contextes d’interface utilisateur prédéfinies, consultez <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>. Pour le  
  
 Si vous souhaitez ouvrir une fenêtre outil dynamique au démarrage et il est possible de l’échec de la création, vous devez implémenter la <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> de l’interface et de tester les conditions d’échec dans le <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> (méthode). Pour l’interpréteur de commandes que vous avez une fenêtre outil dynamique qui doit être ouvert au démarrage, vous devez ajouter le `SupportsDynamicToolOwner` valeur (1) votre enregistrement de package. Cette valeur ne fait pas partie de la norme <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>, vous devez donc créer un attribut personnalisé pour l’ajouter. Pour plus d’informations sur les attributs personnalisés, consultez [à l’aide d’un attribut personnalisé de l’inscription pour inscrire une Extension](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension).  
  
 Utilisez <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> pour ouvrir une fenêtre outil. La fenêtre outil est créée en fonction des besoins.  
  
> [!NOTE]
>  Une fenêtre outil dynamique peut être fermée par l’utilisateur. Si vous souhaitez créer une commande de menu pour l’utilisateur peut rouvrir la fenêtre outil, la commande de menu doit être activée dans le même contexte de l’interface utilisateur qui ouvre la fenêtre outil et désactivée dans le cas contraire.  
  
### <a name="to-open-a-dynamic-tool-window"></a>Pour ouvrir une fenêtre outil dynamique  
  
1.  Créez un projet VSIX nommé **DynamicToolWindow** et ajouter un modèle d’élément de fenêtre outil nommé **DynamicWindowPane.cs**. Pour plus d’informations, consultez [création d’une Extension avec une fenêtre outil](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
2.  Dans le fichier DynamicWindowPanePackage.cs, recherchez la déclaration de DynamicWindowPanePackage. Ajouter le <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> et les attributs T:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute pour inscrire la fenêtre outil.  
  
    ```vb  
    [[ProvideToolWindow(typeof(DynamicWindowPane)]  
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]  
    [Guid(DynamicWindowPanePackageGuids.PackageGuidString)]  
    public sealed class DynamicWindowPanePackage : Package  
    {. . .}  
    ```  
  
     Inscrit la fenêtre Outil nommée DynamicWindowPane sous forme de fenêtre temporaire qui n’est pas conservée lorsque Visual Studio est fermé et rouvert. DynamicWindowPane est ouvert chaque fois que <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> s’applique et fermés dans le cas contraire.  
  
3.  Générez le projet et commencez le débogage. L’instance expérimentale doit apparaître. Vous ne devriez pas voir la fenêtre outil.  
  
4.  Ouvrez un projet dans l’instance expérimentale. La fenêtre outil doit apparaître.