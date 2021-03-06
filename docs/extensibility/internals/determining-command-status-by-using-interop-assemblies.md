---
title: "Déterminer l’état de la commande à l’aide des assemblys d’interopérabilité | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
caps.latest.revision: "18"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3cde6ae841271622e0d538d679991288c111095e
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="determining-command-status-by-using-interop-assemblies"></a>Déterminer l’état de la commande à l’aide des assemblys d’interopérabilité
Un VSPackage doit conserver le suivi de l’état des commandes qu’il peut gérer. L’environnement ne peut pas déterminer quand une commande au sein de votre VSPackage est activée ou désactivée. Il incombe à votre VSPackage pour informer l’environnement à propos des États de la commande, par exemple, l’état général de commandes telles que **couper**, **copie**, et **coller**.  
  
## <a name="status-notification-sources"></a>Sources de Notification d’état  
 L’environnement reçoit des informations sur les commandes via les VSPackages' <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> (méthode), qui fait partie de la mise en œuvre le VSPackage de la <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. L’environnement appelle le <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> méthode du VSPackage sous deux conditions :  
  
-   Lorsqu’un utilisateur ouvre un menu principal ou un menu contextuel (par clic droit), l’environnement exécute la <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> méthode sur toutes les commandes de ce menu pour déterminer leur état.  
  
-   Lorsque le VSPackage demande que l’environnement de mettre à jour l’interface utilisateur actuelle (IU). Cela se produit que les commandes qui sont actuellement visibles par l’utilisateur, tels que les **couper**, **copie**, et **coller** regroupement en fonction de la barre d’outils standard, qui devient activée et désactivée dans réponse aux actions utilisateur et de contexte.  
  
 Étant donné que l’interpréteur de commandes héberge plusieurs packages VS, les performances de l’interpréteur de commandes seraient trop dégrader s’il est nécessaire pour interroger chaque VSPackage pour déterminer l’état de la commande. Au lieu de cela, votre VSPackage doit notifier activement l’environnement lors de son interface utilisateur change au moment de la modification. Pour plus d’informations sur la notification de mise à jour, consultez [mise à jour de l’Interface utilisateur](../../extensibility/updating-the-user-interface.md).  
  
## <a name="status-notification-failure"></a>Échec de Notification d’état  
 Échec de votre VSPackage pour notifier l’environnement un commande de changement d’état peut placer l’interface utilisateur dans un état incohérent. N’oubliez pas que vos commandes de menu menu ou le contexte peuvent être placé sur une barre d’outils par l’utilisateur. Par conséquent, la mise à jour de l’interface utilisateur uniquement quand un menu ou le menu contextuel s’ouvre n’est pas suffisant.  
  
## <a name="see-also"></a>Voir aussi  
 [Comment les VSPackages ajouter les éléments d’Interface utilisateur](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Implémentation](../../extensibility/internals/command-implementation.md)