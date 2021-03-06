---
title: "Comment : déboguer des Workflows basés sur ASP.NET (héritée) | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ASP.NET, debugging workflows
- debugging workflows, ASP.NET workflows
- ASP.NET workflows, debugging
- debugging, ASP.NET workflows
ms.assetid: 79b21edc-9e7d-410d-af68-09c1598b9c30
caps.latest.revision: "5"
author: ErikRe
ms.author: erikre
manager: erikre
ms.openlocfilehash: 0eb248f04119f8f0ad70b9a09a4fb22c73399233
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="how-to-debug-aspnet-based-workflows-legacy"></a>Procédure : déboguer des workflows basés sur ASP.NET (héritée)
Cette rubrique décrit comment déboguer des applications [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] basées sur [!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] qui ciblent le [!INCLUDE[netfx35_long](../workflow-designer/includes/netfx35_long_md.md)] ou le [!INCLUDE[vstecwinfx](../workflow-designer/includes/vstecwinfx_md.md)] dans le [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)] hérité.  
  
 Vous pouvez déboguer des workflows hérités démarrés dans les ASP.NET ou des workflows hérités publiés en tant que services Web en les attachant au processus dans lequel le workflow est hébergé.  
  
### <a name="to-debug-an-aspnet-based-workflow"></a>Pour déboguer des workflows basés sur ASP.NET  
  
1.  Activer le débogage de l’application ASP.NET en affectant **debug = true** dans le fichier web.config.  
  
2.  Définissez la bibliothèque de workflow comme projet de démarrage, et définissez des points d'arrêt sur le workflow.  
  
3.  Entrez l’URL de la page Web par défaut dans les propriétés de projet de flux de travail **déboguer** option **démarrer le navigateur avec l’URL externe** zone de texte.  
  
4.  Sélectionnez **attacher au processus** sur la **déboguer** menu.  
  
5.  Sélectionnez le processus à joindre dans le **processus disponibles** liste.  
  
     Effectuez une jointure au processus w3wp.exe, webdev.webserver, ou aspnet_wp dans lequel le workflow est hébergé.  
  
6.  Cliquez sur **sélectionnez** à côté du **attacher au** zone de texte.  
  
     Le **sélectionner le Type de Code** boîte de dialogue s’affiche.  
  
7.  Sélectionnez **déboguer ces types de codes** et sélectionnez **Workflow**.  
  
8.  Cliquez sur **OK**.  
  
9. Cliquez sur **Attacher**.  
  
10. Ouvrez la page web par défaut dans un navigateur et démarrez le workflow.  
  
## <a name="see-also"></a>Voir aussi  
 [Appel du débogueur Visual Studio pour Windows Workflow Foundation (hérité)](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)   
 [Comment : définir des points d’arrêt dans les Workflows (héritée)](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md)   
 [Débogage de flux de travail hérités](../workflow-designer/debugging-legacy-workflows.md)