---
title: "Priorité de projet | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
caps.latest.revision: "11"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 51ed8cd351a306c3992b4b6c9fcc2231a90085f3
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="project-priority"></a>Priorité de projet
Un élément de projet appartient généralement un seul projet dans la solution. Par conséquent, l’IDE peut déterminer facilement le projet qui est utilisé pour ouvrir l’élément. Toutefois, si un élément est un membre de plusieurs projets, l’IDE utilise un schéma de priorités pour déterminer le projet meilleures pour ouvrir l’élément.  
  
 La liste suivante montre le schéma de priorité de projet :  
  
-   Les appels de l’IDE le <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> méthode pour chaque projet dans la solution pour déterminer si le document est un membre de ce projet.  
  
-   Si le document est un membre du projet, le projet répond avec une priorité que le projet affecte en fonction de sa gestion de ce document. Par exemple, un projet de langage répond avec une priorité élevée pour ses fichiers sources du langage, mais répond avec une priorité plus faible pour un type de fichier non reconnu qui n’est pas utilisé dans le cadre de son processus de génération.  
  
-   Les projets qui fournissent des éditeurs personnalisés, spécifiques à un projet ou les concepteurs pour un document également recevoir une priorité élevée.  
  
-   Le <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> énumération fournit des valeurs de priorité le document.  
  
-   Le projet qui spécifie la priorité la plus élevée est donné le contexte pour ouvrir le document. Si les deux projets de retournent des valeurs de priorité égale, le projet actif est préféré. Si aucun projet de la solution ne répond qu’il puisse ouvrir le document, l’IDE place le document dans le projet fichiers divers. Pour plus d’informations, consultez [le projet fichiers divers](../../extensibility/internals/miscellaneous-files-project.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Projet fichiers divers](../../extensibility/internals/miscellaneous-files-project.md)   
 [Comment : ouvrir les éditeurs pour les Documents ouverts](../../extensibility/how-to-open-editors-for-open-documents.md)   
 [Ajout d’un projet et de modèles d’élément de projet](../../extensibility/internals/adding-project-and-project-item-templates.md)