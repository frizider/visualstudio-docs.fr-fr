---
title: "Implémenter une interface - génération de Code (Visual Basic) | Documents Microsoft"
ms.custom: 
ms.date: 11/17/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bebff2ad-25b6-4adc-8762-60d23bdd639a
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 932cfb092d4106d9afa323aa3689a813ec2dde03
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="implement-an-interface-in-visual-basic"></a>Implémenter une interface en Visual Basic
**Ce que :** vous permet de générer d’immédiatement le code requis pour implémenter une interface. 

**Quand :** vous voulez hériter d’une interface.  

**Pourquoi :** vous pouvez implémenter manuellement de toute l’interface un par un, mais cette fonctionnalité génère automatiquement toutes les signatures de méthode. 

**Comment faire :**

1. Placez votre curseur sur la ligne où il existe une ligne ondulée rouge, indiquant vous avez fait référence à une interface, mais n’avez pas implémenté toutes les membres requis.

   ![Code en surbrillance](media/interface_highlight.png)

1. Ensuite, effectuez l’une des opérations suivantes :
   * **Clavier**
     * Appuyez sur **Ctrl +.** pour déclencher le **Actions rapides et refactorisations** menu et sélectionnez **implémenter l’interface (explicitement)** à partir du message de fenêtre d’aperçu.
   * **Souris**
     * Avec le bouton droit et sélectionnez le **Actions rapides et refactorisations** menu et sélectionnez **implémenter l’interface (explicitement)** à partir du message de fenêtre d’aperçu.
     * Placez le curseur sur la ligne ondulée rouge et cliquez sur le ![Ampoule](media/bulb.png) icône qui s’affiche.
     * Cliquez sur le bouton ![Ampoule](media/bulb.png) icône qui apparaît dans la marge de gauche, si le curseur de texte se trouve déjà sur la ligne de la ligne ondulée rouge.

   ![Aperçu de classe d’implémentation](media/interface_preview.png)

   >[!TIP]
   >Utilisez le [ **aperçu des modifications** ](../../ide/preview-changes.md) lien en bas de la fenêtre d’aperçu pour voir toutes les modifications qui seront apportées avant d’effectuer votre sélection.
   >
   >En outre, vous pouvez utiliser la **Document**, **projet**, et **Solution** liens en bas de la fenêtre d’aperçu pour créer les signatures de méthode approprié sur plusieurs classes qui implémentent l’interface.

1. Les signatures de méthode de l’interface seront créés automatiquement, prêt à être implémentée.

   ![Implémenter le résultat de la classe](media/interface_result.png)

## <a name="see-also"></a>Voir aussi  
[Génération de code (Visual Basic)](../code-generation-vb.md)  
[Aperçu des modifications](../../ide/preview-changes.md)