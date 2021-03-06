---
title: "Débogage des Applications ClickOnce qui utilisent System.Deployment.Application | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
caps.latest.revision: "14"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.openlocfilehash: 19fa51106512394175159c7dd656badaf583dd3c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="debugging-clickonce-applications-that-use-systemdeploymentapplication"></a>Débogage des applications ClickOnce qui utilisent System.Deployment.Application
Dans [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)], [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] déploiement vous permet de configurer la façon dont une application est mise à jour. Toutefois, si vous souhaitez utiliser et personnaliser avancés [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] des fonctionnalités de déploiement, vous devrez accéder au modèle objet de déploiement fourni par <xref:System.Deployment.Application>. Vous pouvez utiliser la <xref:System.Deployment.Application> API pour des tâches avancées telles que :  
  
-   Création d’une option « Mise à jour maintenant » dans votre application  
  
-   Conditionnel, à la demande télécharge des différents composants d’application  
  
-   Intégré directement dans l’application des mises à jour  
  
-   Garantir que l’application cliente est toujours à jour  
  
 Étant donné que la <xref:System.Deployment.Application> API fonctionnent uniquement lorsqu’une application est déployée avec [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] technologie, la seule façon de les déboguer est pour déployer l’application à l’aide de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], attacher à celui-ci, puis déboguer. Il peut être difficile d’attacher le débogueur suffisamment tôt, car ce code s’exécute souvent lors de l’application démarre et s’exécute avant que vous pouvez attacher le débogueur. Une solution consiste à placer des sauts (ou s’arrête, pour les projets Visual Basic) avant votre code de vérification de mise à jour ou le code de la demande.  
  
 La technique de débogage recommandée est la suivante :  
  
1.  Avant de commencer, assurez-vous que les symboles (.pdb) et les fichiers sources sont archivés.  
  
2.  Déployez la version 1 de l’application.  
  
3.  Créez une solution vide. À partir de la **fichier** menu, cliquez sur **nouveau**, puis **projet**. Dans le **nouveau projet** boîte de dialogue, ouvrez le **autres Types de projets** nœud, puis sélectionnez le **Solutions Visual Studio** dossier. Dans le **modèles** volet, sélectionnez **nouvelle Solution**.  
  
4.  Ajoutez l’emplacement source archivé aux propriétés de cette nouvelle solution. Dans **l’Explorateur de solutions**, cliquez sur le nœud solution, puis cliquez sur **propriétés**. Dans le **Pages de propriétés** boîte de dialogue, sélectionnez **déboguer les fichiers sources**, puis ajoutez le répertoire du code source archivé. Sinon, le débogueur recherchera les fichiers sources obsolètes, étant donné que les chemins d’accès du fichier source sont enregistrées dans le fichier .pdb. Si le débogueur utilise des fichiers sources obsolètes, vous consultez un message vous indiquant que la source ne correspond pas.  
  
5.  Assurez-vous que le débogueur peut trouver les fichiers .pdb. Si vous avez déployés avec votre application, le débogueur recherche les automatiquement. Il consulte toujours en regard de l’assembly en question tout d’abord. Dans le cas contraire, vous devez ajouter le chemin d’accès de l’archive le **symbole des emplacements de fichiers (.pdb)** (pour accéder à cette option, à partir de la **outils** menu, cliquez sur **Options**, puis ouvrez le  **Débogage** nœud, puis cliquez sur **symboles**).  
  
6.  Déboguer ce qui se passe entre le `CheckForUpdate` et `Download` / `Update` les appels de méthode.  
  
     Par exemple, le code de mise à jour peut être comme suit :  
  
    ```  
        Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
            If My.Application.Deployment.IsNetworkDeployed Then  
  
                If (My.Application.Deployment.CheckForUpdate()) Then  
  
                    My.Application.Deployment.Update()  
                    Application.Restart()  
  
                End If  
  
            End If  
        End Sub  
    ```  
  
7.  Déployez la version 2.  
  
8.  Essayez d’attacher le débogueur à l’application de la version 1 pendant le téléchargement d’une mise à jour pour la version 2. Vous pouvez également utiliser le `System.Diagnostics.Debugger.Break` méthode ou simplement `Stop` en Visual Basic. Bien entendu, vous ne devez pas laisser ces appels de méthode dans le code de production.  
  
     Par exemple, supposons que vous développez une application Windows Forms, et que vous disposez d’un gestionnaire d’événements pour cette méthode avec la logique de mise à jour qu’elle contient. Pour un débogage, simplement à l’attachement avant que le bouton est enfoncé, puis définissez un point d’arrêt (Assurez-vous que vous ouvrez le fichier archivé approprié et définissez le point d’arrêt).  
  
 Utilisez le <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> propriété à appeler le <xref:System.Deployment.Application> API uniquement lorsque l’application est déployée ; les API ne doivent pas être appelées pendant le débogage dans [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Deployment.Application>