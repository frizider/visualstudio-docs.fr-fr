---
title: "Comment : masquer du texte dans des Documents par programmation | Documents Microsoft"
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
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
ms.assetid: f5ced4ec-22ca-463b-b963-d34ce631b486
caps.latest.revision: "28"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b9ec425a3d83ea088e47725866688ada834ffd34
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>Comment : masquer du texte dans des documents par programmation
  Vous pouvez masquer du texte dans un document en définissant la propriété <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> de <xref:Microsoft.Office.Interop.Word.Range.Font%2A> pour une plage de texte particulière.  
  
 Par exemple, vous pouvez masquer temporairement le texte dans un <xref:Microsoft.Office.Tools.Word.Bookmark> (dans une personnalisation au niveau du document) ou un <xref:Microsoft.Office.Interop.Word.Bookmark> (dans un complément VSTO) avant d’envoyer un document à une imprimante.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
### <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>Pour masquer du texte dans un contrôle Bookmark pendant l’impression du document  
  
1.  Créez une procédure qui masque tout le texte figurant dans une plage spécifiée.  
  
     [!code-vb[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#105)]
     [!code-csharp[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#105)]  
  
2.  Créez une procédure qui affiche tout le texte figurant dans une plage spécifiée.  
  
     [!code-vb[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#106)]
     [!code-csharp[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#106)]  
  
3.  Passez la plage d’un signet à la méthode `HideText` , imprimez le document, puis passez la même plage à la méthode `UnhideText` .  
  
     L'exemple de code suivant peut être utilisé dans une personnalisation au niveau du document. Pour utiliser cet exemple, exécutez-le à partir de la classe `ThisDocument` dans votre projet.  
  
     [!code-vb[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#107)]  
  
     Vous pouvez utiliser l’exemple de code suivant dans un complément VSTO. Cet exemple utilise le document actif. Pour utiliser l'exemple, exécutez-le à partir de la classe `ThisAddIn` dans votre projet.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#107)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Cet exemple de code suppose que le document contient un contrôle <xref:Microsoft.Office.Tools.Word.Bookmark> (dans une personnalisation au niveau du document) ou un contrôle <xref:Microsoft.Office.Interop.Word.Bookmark> (dans un complément VSTO) nommé `bookmark1`.  
  
## <a name="see-also"></a>Voir aussi  
 [Comment : imprimer des Documents par programmation](../vsto/how-to-programmatically-print-documents.md)   
 [Comment : définir par programme et sélectionner des plages dans des Documents](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Comment : réinitialiser des plages dans Word Documents par programmation](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)   
 [Comment : mettre à jour par programme de texte d’un signet](../vsto/how-to-programmatically-update-bookmark-text.md)   
 [Paramètres optionnels dans les solutions Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  