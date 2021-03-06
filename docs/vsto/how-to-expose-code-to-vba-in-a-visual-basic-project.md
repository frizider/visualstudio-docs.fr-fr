---
title: "Comment : exposer du Code à VBA dans un projet Visual Basic | Documents Microsoft"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
ms.assetid: dc74f3ea-3f78-47f8-8a82-a67896144dd9
caps.latest.revision: "47"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 782b42c83f9557b6567849e4d03c7ad9e221da49
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>Comment : exposer du code à VBA dans un projet Visual Basic
  Vous pouvez exposer du code dans un [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projet Visual Basic pour Applications (VBA) si vous souhaitez que les deux types de code interagissent entre eux.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Le processus de Visual Basic est différent du processus Visual c#. Pour plus d’informations, consultez [Comment : exposer du Code à VBA dans un Visual C &#35; Projet](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md).  
  
 Le processus est différent pour le code dans une classe d’élément hôte pour le code dans d’autres classes :  
  
-   [Exposer du code dans une classe d’élément hôte](#HostItemCode)  
  
-   [Exposer du code qui n’est pas dans une classe d’élément hôte](#NonHostItem)  
  
 ![lien vers la vidéo](../vsto/media/playvideo.gif "lien vidéo") pour une démonstration vidéo connexe, consultez [comment faire I: Call VSTO Code à partir de VBA ?](http://go.microsoft.com/fwlink/?LinkId=136757).  
  
##  <a name="HostItemCode"></a>Exposer du Code dans une classe d’élément hôte  
 Pour permettre au code VBA d’appeler du code Visual Basic dans une classe d’élément hôte, définissez le **EnableVbaCallers** propriété de l’élément hôte la valeur **True**.  
  
 Pour une procédure pas à pas qui montre comment exposer une méthode d’une classe d’élément hôte et puis l’appeler à partir de VBA, consultez [procédure pas à pas : appel de Code à partir de VBA dans un projet Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md). Pour plus d’informations sur les éléments hôtes, consultez [Host Items and Host Controls Overview](../vsto/host-items-and-host-controls-overview.md).  
  
#### <a name="to-expose-code-in-a-host-item-to-vba"></a>Pour exposer le code dans un élément hôte à VBA  
  
1.  Ouvrez ou créez au niveau du document [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projet basé sur un document Word, un classeur Excel ou un modèle Excel qui prend en charge les macros et qui contient déjà du code VBA.  
  
     Pour plus d’informations sur les formats de fichier de document qui prennent en charge les macros, consultez [combinaison de VBA et de personnalisations au niveau du Document](../vsto/combining-vba-and-document-level-customizations.md).  
  
    > [!NOTE]  
    >  Cette fonctionnalité ne peut pas être utilisée dans les projets de modèle Word.  
  
2.  Assurez-vous que du code VBA dans le document est autorisé à s’exécuter sans inviter l’utilisateur à activer les macros. Vous pouvez approuver le code VBA à exécuter en ajoutant l'emplacement du projet Office à la liste des emplacements approuvés dans les paramètres du Centre de gestion de la confidentialité pour Word ou Excel.  
  
3.  Ajoutez la propriété, une méthode ou un événement que vous souhaitez exposer à VBA à une des classes d’élément hôte dans votre projet et déclarez le nouveau membre en tant que **Public**. Le nom de la classe dépend de l’application :  
  
    -   Dans un projet Word, la classe d’élément hôte est intitulée `ThisDocument` par défaut.  
  
    -   Dans un projet Excel, les classes d’élément hôte sont nommés `ThisWorkbook`, `Sheet1`, `Sheet2`, et `Sheet3` par défaut.  
  
4.  Définir le **EnableVbaCallers** propriété pour l’élément hôte la valeur **True**. Cette propriété est disponible dans le **propriétés** fenêtre lorsque l’élément hôte est ouvert dans le concepteur.  
  
     Une fois que vous définissez cette propriété, Visual Studio définit automatiquement le **ReferenceAssemblyFromVbaProject** propriété **True**.  
  
    > [!NOTE]  
    >  Si le classeur ou le document ne contient pas déjà du code VBA, ou si le code VBA dans le document n’est pas approuvé, vous recevrez un message d’erreur lorsque vous définissez la **EnableVbaCallers** propriété **True**. Cela est dû au fait que Visual Studio ne peut pas modifier le projet VBA dans le document dans cette situation.  
  
5.  Cliquez sur **OK** dans le message qui s'affiche. Ce message vous rappelle que si vous ajoutez du code VBA au classeur ou au document lors vous exécutez le projet à partir de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], le code VBA seront perdu lors de la prochaine fois que vous générez le projet. Il s’agit, car le document dans le dossier de sortie de génération est remplacé chaque fois que vous générez le projet.  
  
     À ce stade, Visual Studio configure le projet afin que le projet VBA peut appeler l’assembly. Visual Studio ajoute également une propriété nommée `CallVSTOAssembly` à la `ThisDocument`, `ThisWorkbook`, `Sheet1`, `Sheet2`, ou `Sheet3` module dans le projet VBA. Vous pouvez utiliser cette propriété pour accéder aux membres publics de la classe que vous avez exposée à VBA.  
  
6.  Générez le projet.  
  
##  <a name="NonHostItem"></a>Exposer du Code qui n’est pas dans une classe d’élément hôte  
 Pour permettre au code VBA d’appeler du code Visual Basic qui n’est pas dans une classe d’élément hôte, modifiez le code afin qu’il est visible à VBA.  
  
#### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>Pour exposer le code qui n’est pas dans une classe d’élément hôte à VBA  
  
1.  Ouvrez ou créez au niveau du document [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projet basé sur un document Word, un classeur Excel ou un modèle Excel qui prend en charge les macros et qui contient déjà du code VBA.  
  
     Pour plus d’informations sur les formats de fichier de document qui prennent en charge les macros, consultez [combinaison de VBA et de personnalisations au niveau du Document](../vsto/combining-vba-and-document-level-customizations.md).  
  
    > [!NOTE]  
    >  Cette fonctionnalité ne peut pas être utilisée dans les projets de modèle Word.  
  
2.  Assurez-vous que du code VBA dans le document est autorisé à s’exécuter sans inviter l’utilisateur à activer les macros. Vous pouvez approuver le code VBA à exécuter en ajoutant l'emplacement du projet Office à la liste des emplacements approuvés dans les paramètres du Centre de gestion de la confidentialité pour Word ou Excel.  
  
3.  Ajouter le membre que vous souhaitez exposer à VBA à une classe publique dans votre projet et déclarez le nouveau membre en tant que **public**.  
  
4.  Appliquez ce qui suit <xref:System.Runtime.InteropServices.ComVisibleAttribute> et <xref:Microsoft.VisualBasic.ComClassAttribute> des attributs à la classe que vous exposez à VBA. Ces attributs rendent la classe visible pour VBA.  
  
    ```vb  
    <Microsoft.VisualBasic.ComClass()> _  
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _  
    ```  
  
5.  Substituez la méthode **GetAutomationObject** d'une classe d'élément hôte de votre projet pour retourner une instance de la classe que vous exposez à VBA. L’exemple de code suivant suppose que vous exposez une classe nommée `DocumentUtilities` à VBA.  
  
    ```vb  
    Protected Overrides Function GetAutomationObject() As Object  
        Return New DocumentUtilities()  
    End Function  
    ```  
  
6.  Ouvrez le document (pour Word) ou le Concepteur de feuille de calcul (pour Excel) dans [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
7.  Dans la fenêtre **Propriétés** , sélectionnez la propriété **ReferenceAssemblyFromVbaProject** et remplacez sa valeur par **True**.  
  
    > [!NOTE]  
    >  Si le classeur ou le document ne contient pas déjà du code VBA, ou si le code VBA dans le document n’est pas approuvé, vous recevrez un message d’erreur lorsque vous définissez la **ReferenceAssemblyFromVbaProject** propriété **True** . Cela est dû au fait que Visual Studio ne peut pas modifier le projet VBA dans le document dans cette situation.  
  
8.  Cliquez sur **OK** dans le message qui s'affiche. Ce message vous rappelle que si vous ajoutez du code VBA au classeur ou au document lors vous exécutez le projet à partir de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], le code VBA seront perdu lors de la prochaine fois que vous générez le projet. Il s’agit, car le document dans le dossier de sortie de génération est remplacé chaque fois que vous générez le projet.  
  
     À ce stade, Visual Studio configure le projet afin que le projet VBA peut appeler l’assembly. Visual Studio ajoute également une méthode nommée `GetManagedClass` au projet VBA. Vous pouvez appeler cette méthode à partir de n’importe où dans le projet VBA pour accéder à la classe que vous avez exposée à VBA.  
  
9. Générez le projet.  
  
## <a name="see-also"></a>Voir aussi  
 [Comment : créer des projets Office dans Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Conception et création de Solutions Office](../vsto/designing-and-creating-office-solutions.md)   
 [Combining VBA and Document-Level Customizations](../vsto/combining-vba-and-document-level-customizations.md)   
 [Procédure pas à pas : Appel de Code à partir de VBA dans un projet Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)   
 [Comment : exposer du Code à VBA dans un Visual C &#35; Projet](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)  
  
  