---
title: Validation de bloc graphique | Documents Microsoft
ms.custom: 
ms.date: 03/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.graphics.FrameValidation
ms.assetid: 1e639182-1301-4e28-9c1e-b5df732f3f1b
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9312ad8a96c5829aae21c87e78a0d5f2f0db1b35
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="graphics-frame-validation"></a>Validation des frames graphiques
<!-- VERSIONLESS -->
Visual Studio 2017 et une prise en charge la **Frame Validation** outil.  La fenêtre Frame Validation affiche des erreurs et avertissements associés à la liste des événements.  Pour afficher cette fenêtre, sélectionnez le **vue > Frame Validation** menu.

![Validation de frame](media/gfx_diag_frame_validation.png)

Cliquez sur le **exécuter la Validation** bouton dans l’angle supérieur gauche pour lancer l’analyse.  Il peut prendre plusieurs minutes selon la complexité de l’image.  Les données qui s’affiche ici est une combinaison de deux sources : les messages que D3D lui-même émet lorsque [couches SDK](https://msdn.microsoft.com/library/windows/desktop/ff476881(v=vs.85).aspx) est activé et les données collectées à partir de l’état interne de l’outil de suivi. Une fois terminé, vous voyez plusieurs colonnes de données :

**Colonne**|**Description**
---|---
ID d'événement | ID qui est mappée à une entrée dans le [liste des événements](graphics-event-list.md) fenêtre.
Gravité | Endommagement, erreur, avertissement, information ou Message.
Catégorie | Application définie, divers, d’initialisation, nettoyage, Compilation, la création de l’état, paramètre état, l’obtention de l’état, l’exécution, Manipulation des ressources, nuanceur, redondant et non utilisé.
Message | Le message associé à l’événement.
Événement | L’événement associé à l’erreur ou l’avertissement.

## <a name="see-also"></a>Voir aussi  
[Graphics Diagnostics (débogage DirectX Graphics)](visual-studio-graphics-diagnostics.md)   
<!-- /VERSIONLESS -->