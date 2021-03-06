---
title: "Démarrage rapide : Créer une application console dans Visual Studio avec Visual Basic | Microsoft Docs"
ms.custom: 
ms.date: 12/05/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-acquisition
ms.tgt_pltfrm: 
ms.topic: quickstart
ms.devlang: vb
author: TerryGLee
ms.author: tglee
manager: ghogen
dev_langs: vb
ms.openlocfilehash: 57441895ccff8bf32b59d6306ca4ae618382d356
ms.sourcegitcommit: 38097344f3ff74ba7b03bcfa45910015ca6bc2be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="quickstart-create-a-console-app-in-visual-studio-with-visual-basic"></a>Démarrage rapide : Créer une application console dans Visual Studio avec Visual Basic
Dans cette présentation de 5-10 minutes de l’environnement de développement intégré (IDE) de Visual Studio, vous allez créer une application Visual Basic simple qui s’exécute dans la console.

Si vous n’avez pas encore installé Visual Studio, accédez à la page [Téléchargements Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) pour l’installer gratuitement.

## <a name="create-a-project"></a>Créer un projet
Tout d’abord, vous allez créer un projet d’application Visual Basic. Le type de projet inclut tous les fichiers de modèle dont vous aurez besoin au départ.

1. Ouvrez Visual Studio 2017.

2. Dans la barre de menus supérieure, choisissez **Fichier** > **Nouveau** > **Projet...**.

3. Dans la boîte de dialogue **Nouveau projet**, dans le volet gauche, développez **Visual Basic**, puis choisissez **.NET Core**. Dans le volet central, choisissez **Application console (.NET Core)**. Ensuite, nommez le projet *HelloWorld*.

   ![Charge de travail Développement multiplateforme .Net Core dans Visual Studio Installer](../ide/media/new-project-vb-dotnet-helloworld-console-app.png)

     Si vous ne voyez pas le modèle de projet **Application console (.NET Core)**, cliquez sur le lien **Ouvrir Visual Studio Installer** dans le volet gauche de la boîte de dialogue **Nouveau projet**.

   ![Cliquer sur le lien Ouvrir Visual Studio Installer dans la boîte de dialogue Nouveau projet](../ide/media/vb-open-visual-studio-installer.png)

     Visual Studio Installer est lancé. Choisissez la charge de travail **Développement multiplateforme .NET Core**, puis choisissez **Modifier**.

     ![Charge de travail Développement multiplateforme .Net Core dans Visual Studio Installer](../ide/media/dot-net-core-xplat-dev-workload.png)

## <a name="create-the-application"></a>Créer l’application
Une fois que vous avez sélectionné votre modèle de projet Visual Basic et nommé votre projet, Visual Studio crée une application « Hello World » simple. Il appelle la méthode [Console.WriteLine(System.String)](https://docs.microsoft.com/en-us/dotnet/api/system.console.writeline?view=netframework-4.7.1#System_Console_WriteLine_System_String) pour afficher la chaîne littérale « Hello World ! » dans la fenêtre de console.

![Afficher le code Hello World par défaut à partir du modèle](../ide/media/vb-console-helloworld-template.png)

Si vous cliquez sur le bouton **HelloWorld** dans l’IDE, vous exécutez le programme en mode débogage.

  ![Cliquer sur le bouton Hello World pour exécuter le programme en mode débogage](../ide/media/vb-console-hello-world-button.png)

Dans ce cas, la fenêtre de console reste visible seulement un instant avant sa fermeture. Cela s’explique par le fait que la méthode `Main` se termine après l’exécution de son instruction unique, entraînant la fin de l’application.

### <a name="add-some-code"></a>Ajouter du code
Vous allez maintenant ajouter du code pour suspendre l’application et demander une entrée utilisateur.

1. Ajoutez le code suivant immédiatement après l’appel de la méthode [Console.WriteLine(System.String)](https://docs.microsoft.com/en-us/dotnet/api/system.console.writeline?view=netframework-4.7.1#System_Console_WriteLine_System_String) :

   ```vb
   Console.Write("Press any key to continue...")
   Console.ReadKey(true)
   ```
   Le programme est alors suspendu jusqu’à ce que l’utilisateur appuie sur une touche.

2. Dans la barre de menus, sélectionnez **Générer** > **Générer la solution**.

   Ceci compile votre programme en un langage intermédiaire, qui est ensuite converti en code binaire par un compilateur juste-à-temps (JIT).

## <a name="run-the-application"></a>Exécuter l'application
1. Cliquez sur le bouton **HelloWorld** dans la barre d’outils.

   ![Cliquer sur le bouton Hello World pour exécuter le programme à partir de la barre d’outils](../ide/media/vb-console-hello-world-button.png)

2. Appuyez sur une touche pour fermer la fenêtre de console.

   ![Fenêtre de console affichant « Hello World » et « Press any key to continue »](../ide/media/vb-console-hello-world-press-any-key.png)

Félicitations ! Vous avez terminé ce guide de démarrage rapide. Nous espérons que vous en avez appris un peu plus sur Visual Basic et l’IDE de Visual Studio. Si vous souhaitez approfondir ce sujet, poursuivez avec un didacticiel que vous trouverez dans la section **Didacticiels** de la table des matières.

## <a name="see-also"></a>Voir aussi
* [Démarrage rapide : Créer une application Windows Forms « Hello World » dans Visual Studio avec Visual Basic](quickstart-visual-basic-winforms.md)
* [En savoir plus sur Visual Basic IntelliSense](visual-basic-specific-intellisense.md)
