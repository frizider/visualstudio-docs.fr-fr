---
title: "Comment : réduire des plages par programmation ou des sélections dans des Documents | Documents Microsoft"
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
- selections, collapsing
- documents [Office development in Visual Studio], collapsing ranges
- collapsing selections
- ranges, collapsing
- collapsing ranges
ms.assetid: 0bd059dd-8606-42ae-a8a9-97f8f3bd5cc5
caps.latest.revision: "42"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 89430ca1b20df29bbd29af4ef41ceb7a9182564e
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>Comment : réduire des plages ou des sélections dans des documents par programmation
  Si vous travaillez avec un objet <xref:Microsoft.Office.Interop.Word.Range> ou <xref:Microsoft.Office.Interop.Word.Selection> , vous pouvez remplacer la sélection par un point d’insertion avant d’insérer du texte, afin d’éviter de remplacer le texte existant. À la fois le <xref:Microsoft.Office.Interop.Word.Range> et <xref:Microsoft.Office.Interop.Word.Selection> objets ont une méthode Collapse, qui utilise le <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> valeurs d’énumération :  
  
-   <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> réduit la sélection au début de la sélection. Il s’agit de la valeur par défaut si vous ne spécifiez pas de valeur d’énumération.  
  
-   <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> réduit la sélection à la fin de la sélection.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
### <a name="to-collapse-a-range-and-insert-new-text"></a>Pour réduire une plage et insérer un nouveau texte  
  
1.  Créez un objet <xref:Microsoft.Office.Interop.Word.Range> constitué du premier paragraphe du document.  
  
     L’exemple de code suivant peut être utilisé dans une personnalisation au niveau du document.  
  
     [!code-vb[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#46)]
     [!code-csharp[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#46)]  
  
     Vous pouvez utiliser l’exemple de code suivant dans un complément VSTO. Ce code utilise le document actif.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#46)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#46)]  
  
2.  Utilisez la valeur d’énumération <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> pour réduire la plage.  
  
     [!code-vb[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#47)]
     [!code-csharp[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#47)]  
  
3.  Insérez le nouveau texte.  
  
     [!code-vb[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#48)]
     [!code-csharp[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#48)]  
  
4.  Sélectionnez le contrôle <xref:Microsoft.Office.Interop.Word.Range>.  
  
     [!code-vb[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#49)]
     [!code-csharp[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#49)]  
  
 Si vous utilisez la valeur d’énumération <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> , le texte est inséré au début du paragraphe suivant.  
  
 [!code-vb[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#50)]
 [!code-csharp[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#50)]  
  
 Vous pourriez vous attendre à ce que l’insertion d’une nouvelle phrase se fasse avant la marque de paragraphe, mais ce n’est pas le cas, car celle-ci est incluse dans la plage d’origine. Pour plus d’informations, consultez [Comment : par programme exclure paragraphe marques lors de la création de plages](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md).  
  
## <a name="document-level-customization-example"></a>Exemple de personnalisation au niveau du document  
  
#### <a name="to-collapse-a-range-in-a-document-level-customization"></a>Pour réduire une plage dans une personnalisation au niveau du document  
  
1.  L’exemple suivant affiche la méthode complète correspondant à la personnalisation au niveau du document. Pour utiliser ce code, exécutez-le à partir de la classe `ThisDocument` de votre projet.  
  
     [!code-vb[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#45)]  
  
## <a name="vsto-add-in-example"></a>Exemple de complément VSTO  
  
#### <a name="to-collapse-a-range-in-an-vsto-add-in"></a>Pour réduire une plage dans un complément VSTO  
  
1.  L’exemple suivant affiche la méthode complète correspondant à un complément VSTO. Pour utiliser ce code, exécutez-le à partir de la classe `ThisAddIn` de votre projet.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#45)]  
  
## <a name="see-also"></a>Voir aussi  
 [Comment : insérer du texte dans des Documents Word par programmation](../vsto/how-to-programmatically-insert-text-into-word-documents.md)   
 [Comment : définir par programme et sélectionner des plages dans des Documents](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Comment : récupérer les caractères de début et fin dans les plages par programmation](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)   
 [Comment : exclure les marques de paragraphe par programmation lorsque vous créez des plages](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)   
 [Comment : étendre des plages dans des Documents par programmation](../vsto/how-to-programmatically-extend-ranges-in-documents.md)   
 [Guide pratique pour réinitialiser des plages dans les documents Word par programmation](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)  
  