---
title: "Comment : déboguer un Service WCF auto-hébergé | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, self-hosted service
- WCF, debugging
ms.assetid: 288922be-ba3f-411e-af50-bba39c9529cc
caps.latest.revision: "25"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e64f764153106c252ba1a9586bfd0a33f4e239f4
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-debug-a-self-hosted-wcf-service"></a>Comment : déboguer un service WCF auto-hébergé
A *service auto-hébergé* est un service WCF qui ne s’exécute pas à l’intérieur d’IIS, l’hôte de Service WCF ou [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] serveur de développement. Pour déboguer un service WCF auto-hébergé le plus simple consiste à configurer [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] pour lancer le client et le serveur lorsque vous choisissez **démarrer le débogage** sur la **déboguer** menu.  
  
 Si le service WCF est auto-hébergé dans un processus qui ne peut pas être lancé de cette manière, tels que service NT, vous ne pouvez pas utiliser cette méthode. Au lieu de cela, vous pouvez effectuer une des opérations suivantes :  
  
-   Attacher manuellement le débogueur au processus d’hébergement. Pour plus d’informations, consultez [attacher au processus en cours](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
     — ou —  
  
-   Démarrer le débogage du client et puis pas à pas détaillé d’un appel au service. Cela nécessite que vous activez le débogage dans le fichier app.config. Pour plus d’informations, [Limitations du débogage WCF](../debugger/limitations-on-wcf-debugging.md).  
  
### <a name="to-start-both-client-and-host-from-visual-studio"></a>Pour démarrer des clients et hôtes à partir de Visual Studio  
  
1.  Créer un [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] solution qui contient à la fois les projets client et serveur.  
  
2.  Configurer la solution pour démarrer le processus client et serveur lorsque vous choisissez **Démarrer** sur la **déboguer** menu.  
  
    1.  Dans **l’Explorateur de solutions**, cliquez sur le nom de la solution.  
  
    2.  Cliquez sur **définir les projets de démarrage**.  
  
    3.  Dans le **Solution \<nom > Propriétés** boîte de dialogue, sélectionnez **plusieurs projets de démarrage**.  
  
    4.  Dans le **plusieurs projets de démarrage** grille, dans la ligne qui correspond au projet serveur, cliquez sur **Action** et choisissez **Démarrer**.  
  
    5.  Sur la ligne qui correspond au projet client, cliquez sur **Action** et choisissez **Démarrer**.  
  
    6.  Cliquez sur **OK**.  
  
## <a name="see-also"></a>Voir aussi  
 [Débogage de Services WCF](../debugger/debugging-wcf-services.md)   
 [Limitations du débogage WCF](../debugger/limitations-on-wcf-debugging.md)   
 [Guide pratique pour effectuer un pas à pas détaillé dans les services WCF](../debugger/how-to-step-into-wcf-services.md)