---
title: "Guide pratique pour spécifier une icône d’application (Visual Basic, C#) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- icons [Visual Studio], application
- application properties [Visual Studio], icons
- application icons [Visual Studio]
ms.assetid: ad8e14ed-adc2-45b6-a0be-818b16d5616f
caps.latest.revision: "18"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 17cce04dd94829225823de676e286b7d0158abec
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-specify-an-application-icon-visual-basic-c"></a>Guide pratique pour spécifier une icône d'application (Visual Basic, C#)
La propriété `Icon` d'un projet spécifie le fichier de l'icône (.ico) qui sera affichée pour l'application compilée dans l'Explorateur de fichiers et dans la barre des tâches Windows.  
  
 La propriété `Icon` est accessible dans le volet **Application** du **Concepteur de projet**. Elle contient une liste des icônes qui ont été ajoutées à un projet comme ressources ou comme fichiers de contenu.  
  
> [!NOTE]
>  Après avoir défini la propriété Icon pour une application, vous pouvez également définir la propriété `Icon` de chaque **Fenêtre** ou **Formulaire** de l’application. Pour plus d'informations sur les icônes de fenêtre pour les applications autonomes Windows Presentation Foundation (WPF), consultez la propriété <xref:System.Windows.Window.Icon%2A>.  
  
### <a name="to-specify-an-application-icon"></a>Pour spécifier une icône d'application  
  
1.  Dans l’**Explorateur de solutions**, choisissez un nœud de projet (pas le nœud **Solution**).  
  
2.  Dans la barre de menus, choisissez **Projet**, **Propriétés**.  
  
3.  Quand le **Concepteur de projet** apparaît, choisissez l’onglet **Application**.  
  
4.  **(Visual Basic)** Dans la liste **Icône**, sélectionnez un fichier icône (.ico).  
  
     **C#** À côté de la liste **Icône**, choisissez le bouton **\<Parcourir...>**, puis accédez à l’emplacement du fichier icône souhaité.  
  
## <a name="see-also"></a>Voir aussi  
 [Page Application, Concepteur de projets (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)   
 [Page Application, Concepteur de projets (C#)](../ide/reference/application-page-project-designer-csharp.md)   
 [Gestion des propriétés de l’application](../ide/application-properties.md)  
 [Guide pratique pour ajouter ou supprimer des ressources](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)