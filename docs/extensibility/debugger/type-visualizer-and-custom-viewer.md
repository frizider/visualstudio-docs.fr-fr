---
title: "Type du visualiseur et la visionneuse personnalisée | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
caps.latest.revision: "13"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 80798887beee6116b3a93b5d8ec86b14269b5475
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="type-visualizer-and-custom-viewer"></a>Visualiseur de type et de la visionneuse personnalisée
Un visualiseur de type est un composant qui affiche un élément de données dans un format très spécifique. Ce format est entièrement à l’implémenteur du visualiseur, soit l’utilisateur final ou un fournisseur tiers de visualiseurs.  
  
 Une visionneuse personnalisée est la partie d’un évaluateur d’expression personnalisée qui affiche un élément de données dans un format très spécifique. Ce format est entièrement à l’implémenteur de la visionneuse personnalisée, ce qui signifie que le format est à l’implémenteur de l’évaluateur d’expression (EE).  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>Prise en charge des visualiseurs de types dans l’évaluateur d’Expression  
 Un EE peut prendre en charge les visualiseurs de types en prenant en charge un ensemble d’interfaces accessibles aux visualiseurs : interfaces telles que [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) et [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md). Notez, toutefois, que le EE n’est pas chargé d’implémenter le visualiseur de type lui-même : le EE permet simplement visualiseurs externes d’accéder à ses informations de type. Ces visualiseurs peuvent livrés avec le Java EE et installés dans l’emplacement approprié dans Visual Studio, fournis par un autre fournisseur tiers, ou même par l’utilisateur final.  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>Prise en charge des visionneuses personnalisées dans l’évaluateur d’Expression  
 Un EE peut également gérer les visionneuses personnalisées dans laquelle le EE lui-même fournit le code pour afficher le type de données. Une visionneuse personnalisée implémente la [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) interface qui gère toutes les tâches de l’affichage des données dans le format d’est souhaitée ; a un contrôle total sur l’affichage de la visionneuse et peut même permettre les modification des données. Les visionneuses personnalisées fournies par le EE sont fournis avec le Java EE lorsque le produit est fourni.  
  
## <a name="see-also"></a>Voir aussi  
 [Composants du débogueur](../../extensibility/debugger/debugger-components.md)   
 [Évaluateur d’expression](../../extensibility/debugger/expression-evaluator.md)   
 [Moteur de débogage](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)