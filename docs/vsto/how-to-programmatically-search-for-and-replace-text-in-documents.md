---
title: "Comment : rechercher par programmation et remplacer du texte dans des Documents | Documents Microsoft"
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
- documents [Office development in Visual Studio], searching
- text searches, replacing text
- text searches, documents
- text [Office development in Visual Studio], searching in documents
- text [Office development in Visual Studio], text searches
ms.assetid: a66962f5-eeb9-4dc6-a70f-9039ab437a63
caps.latest.revision: "51"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4d3b5523bdf6d851f7822a7123575b2903b45a2a
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-programmatically-search-for-and-replace-text--in-documents"></a>Comment : rechercher et remplacer du texte dans les documents par programmation
  L'objet <xref:Microsoft.Office.Interop.Word.Find> est membre des objets <xref:Microsoft.Office.Interop.Word.Selection> et <xref:Microsoft.Office.Interop.Word.Range>, que vous pouvez utiliser indifféremment pour rechercher du texte dans des documents Microsoft Office Word. La commande Replace est une extension de la commande Find.  
  
 Utilisez un objet <xref:Microsoft.Office.Interop.Word.Find> pour parcourir un document Microsoft Office Word et rechercher du texte, une mise en forme ou un style spécifique, et utilisez la propriété <xref:Microsoft.Office.Interop.Word.Find.Replacement%2A> pour remplacer l'un des éléments trouvés.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="using-a-selection-object"></a>Utilisation d'un objet Selection  
 Quand vous utilisez un objet <xref:Microsoft.Office.Interop.Word.Selection> pour rechercher du texte, les critères de recherche que vous spécifiez s'appliquent uniquement au texte sélectionné. Si l'objet <xref:Microsoft.Office.Interop.Word.Selection> est un point d'insertion, la recherche s'effectue dans le document. Quand l'élément correspondant aux critères de recherche est trouvé, il est automatiquement sélectionné.  
  
 Il est important de noter que les critères <xref:Microsoft.Office.Interop.Word.Find> sont cumulatifs, ce qui signifie qu'ils sont ajoutés aux critères de recherche précédents. Avant la recherche, effacez la mise en forme des recherches précédentes à l'aide de la méthode <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A>.  
  
#### <a name="to-find-text-using-a-selection-object"></a>Pour rechercher du texte à l'aide d'un objet Selection  
  
1.  Affectez une chaîne de recherche à une variable.  
  
     [!code-vb[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#68)]
     [!code-csharp[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#68)]  
  
2.  Effacez la mise en forme des recherches précédentes.  
  
     [!code-vb[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#69)]
     [!code-csharp[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#69)]  
  
3.  Exécutez la recherche et affichez une boîte de message avec les résultats.  
  
     [!code-vb[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#70)]
     [!code-csharp[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#70)]  
  
 L'exemple suivant montre la méthode complète.  
  
 [!code-vb[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#67)]
 [!code-csharp[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#67)]  
  
## <a name="using-a-range-object"></a>Utilisation d'un objet Range  
 L'utilisation d'un objet <xref:Microsoft.Office.Interop.Word.Range> vous permet de rechercher du texte sans rien afficher dans l'interface utilisateur. Le <xref:Microsoft.Office.Interop.Word.Find> retourne l’objet **True** si le texte est trouvé, qui correspond aux critères de recherche, et **False** si elle n’est pas le cas. Il redéfinit également l'objet <xref:Microsoft.Office.Interop.Word.Range> pour qu'il corresponde aux critères de recherche si le texte est trouvé.  
  
#### <a name="to-find-text-using-a-range-object"></a>Pour rechercher du texte à l'aide d'un objet Range  
  
1.  Définissez un objet <xref:Microsoft.Office.Interop.Word.Range> constitué du deuxième paragraphe du document.  
  
     L'exemple de code suivant peut être utilisé dans une personnalisation au niveau du document.  
  
     [!code-vb[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#72)]
     [!code-csharp[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#72)]  
  
     L'exemple de code suivant peut être utilisé dans un complément VSTO. Cet exemple utilise le document actif.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#72)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#72)]  
  
2.  À l’aide de la <xref:Microsoft.Office.Interop.Word.Range.Find%2A> propriété de la <xref:Microsoft.Office.Interop.Word.Range> de l’objet, désactivez d’abord toutes les options de mise en forme existantes, puis recherchez la chaîne **me trouver**.  
  
     [!code-vb[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#73)]
     [!code-csharp[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#73)]  
  
3.  Affichez les résultats de la recherche dans une boîte de message, puis sélectionnez l'objet <xref:Microsoft.Office.Interop.Word.Range> pour le rendre visible.  
  
     [!code-vb[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#74)]
     [!code-csharp[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#74)]  
  
     Si la recherche échoue, le deuxième paragraphe est sélectionné. Si elle réussit, les critères de recherche sont affichés.  
  
 L'exemple suivant montre le code complet pour une personnalisation au niveau du document. Pour utiliser cet exemple, exécutez le code à partir de la classe `ThisDocument` dans votre projet.  
  
 [!code-vb[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#71)]
 [!code-csharp[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#71)]  
  
 L’exemple suivant montre le code complet pour un complément VSTO. Pour utiliser cet exemple, exécutez le code à partir de la classe `ThisAddIn` dans votre projet.  
  
 [!code-vb[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#71)]
 [!code-csharp[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#71)]  
  
## <a name="searching-for-and-replacing-text-in-documents"></a>Recherche et remplacement de texte dans des documents  
 Le code suivant recherche la sélection actuelle et remplace toutes les occurrences de la chaîne **me trouver** avec la chaîne **trouvé**.  
  
#### <a name="to-search-for-and-replace-text-in-documents"></a>Pour rechercher et remplacer du texte dans des documents  
  
1.  Ajoutez l'exemple de code suivant à la classe `ThisDocument` ou `ThisAddIn` dans votre projet.  
  
     [!code-vb[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#75)]
     [!code-csharp[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#75)]  
  
     La classe <xref:Microsoft.Office.Interop.Word.Find> a une méthode <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> et la classe <xref:Microsoft.Office.Interop.Word.Replacement> a également sa propre méthode <xref:Microsoft.Office.Interop.Word.Replacement.ClearFormatting%2A>. Quand vous effectuez des opérations de recherche et remplacement, vous devez utiliser la méthode ClearFormatting des deux objets. Si vous l'utilisez uniquement sur l'objet <xref:Microsoft.Office.Interop.Word.Find>, vous pouvez obtenir des résultats inattendus dans le texte de remplacement.  
  
2.  Utilisez la méthode <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> de l'objet <xref:Microsoft.Office.Interop.Word.Find> pour remplacer chaque élément trouvé. Pour spécifier les éléments à remplacer, utilisez le *remplacer* paramètre. Ce paramètre peut avoir l'une des valeurs <xref:Microsoft.Office.Interop.Word.WdReplace> suivantes :  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceAll> remplace tous les éléments trouvés.  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceNone> ne remplace aucun des éléments trouvés.  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceOne> remplace le premier élément trouvé.  
  
## <a name="see-also"></a>Voir aussi  
 [Comment : définir les Options de recherche dans Word par programmation](../vsto/how-to-programmatically-set-search-options-in-word.md)   
 [Comment : Parcourir par programmation des éléments trouvés dans des Documents](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)   
 [Comment : définir par programme et sélectionner des plages dans des Documents](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Comment : restaurer des sélections après des recherches de par programmation](../vsto/how-to-programmatically-restore-selections-after-searches.md)   
 [Paramètres optionnels dans les solutions Office](../vsto/optional-parameters-in-office-solutions.md)  
  