---
title: "Présentation des configurations de build"
description: 
author: asb3993
ms.author: amburns
ms.date: 04/14/2017
ms.topic: article
ms.assetid: 78107CFA-9308-4293-A92A-9B552A259E15
ms.openlocfilehash: e435418c0c77f1577e9db8ab35d76d6bd54f8447
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="understanding-build-configurations"></a>Présentation des configurations de build

## <a name="project-build-configurations"></a>Configurations de build d’un projet 

Les projets peuvent avoir plusieurs configurations, et passer de l’une à l’autre permet différentes sorties au moment de la génération. Par exemple, lors de l’utilisation d’une configuration Debug, la sortie comprend des symboles de débogage, ce qui permet au débogueur de résoudre les noms de fonction, les paramètres ou les variables à partir de la trace de la pile d’une application qui s’est bloquée. Cependant, l’utilisation d’une configuration Debug a pour conséquence une augmentation de la taille des fichiers et ne conviendrait donc pas pour une application destinée à être distribuée.

Chaque plateforme a des configurations spécifiques pour sa génération. Le développement Xamarin.Android sera toujours limité à une configuration Debug ou une configuration Release. Xamarin.iOS a plus de configurations. Les projets iOS plus récents ont seulement des configurations Debug ou Release, mais celles-ci peuvent être définies pour un appareil ou pour n’importe quel simulateur installé.

## <a name="solution-configurations"></a>Configurations de solution

Comme pour les configurations de projet, les configurations de solution sont utilisées pour créer des configurations personnalisées pour un projet entier. Sous l’onglet **Mappages de configuration** sous l’élément **Build > Configurations**, vous pouvez affecter une configuration cible pour chaque élément de la solution, comme illustré ci-dessous :


 ![Options de mappage de configuration](media/projects-and-solutions-image3.png)

Pour plus d’informations, reportez-vous à la vidéo [Configuration Manager](https://www.youtube.com/watch?v=tjSdkqYh5Vg) de James Montemagno.

## <a name="run-configuration"></a>Configuration d’exécution

Dans les versions précédentes de Xamarin Studio, vous pouviez sélectionner une option pour définir un projet en tant que **Projet de démarrage**, qui est le projet exécuté/débogué quand vous utilisez la commande générale exécuter/déboguer. Le nom du projet était indiqué en gras dans le panneau des projets.

Dans Visual Studio pour Mac, au lieu de définir un projet de démarrage, vous pouvez définir une _configuration d’exécution_. Les configurations d’exécution sont présentées dans une liste déroulante dans la barre d’outils, en regard du sélecteur de configuration de build, comme illustré ci-dessous :

 ![Listé déroulante Configuration d’exécution](media/projects-and-solutions-image8.png)

Une configuration d’exécution est un ensemble d’options d’exécution avec un nom et plusieurs configurations qui sont définies dans un projet à des fins différentes. Les configurations d’exécution sont définies au niveau du projet, et une configuration par défaut est créée automatiquement pour chaque projet exécutable, même s’il est possible d’en ajouter autant que nécessaire. Certains types de projets génèrent automatiquement des configurations d’exécution supplémentaires. Par exemple, les projets watchOS peuvent générer des _configurations Coup d’œil et Notification_. 
 
Vous pouvez partager les configurations avec d’autres développeurs (auquel cas, elles sont stockées dans le fichier .csproj) ou les conserver localement (auquel cas, elles sont stockées dans un fichier .user).

### <a name="android-run-configurations"></a>Configurations d’exécution Android
 
Les configurations d’exécution pour les projets Android vous permettent de spécifier l’activité, le service ou le récepteur de diffusion qui doit être lancé lors de l’exécution ou du débogage du projet. Vous pouvez passer des données supplémentaires intentionnelles et définir des indicateurs intentionnels pour pouvoir tester vos composants dans différentes conditions de lancement.

Pour le débogage sur un appareil physique, vous devez ajouter `Exported=true` à l’attribut Activity pour les activités autres que `MainLauncher` ou définir des filtres intentionnels.

## <a name="examples-of-data-that-might-be-included-in-run-configurations"></a>Exemples de données pouvant être incluses dans les configurations d’exécution

La liste ci-dessous fournit quelques exemples de données qui peuvent être incluses dans les configurations d’exécution :

* Projet .NET normal
    * Application de démarrage alternative
    * Arguments du démarrage
    * Répertoire de travail
    * Variables d’environnement
    * Options de runtime Mono (à utiliser uniquement lors de l’exécution sur Mono)
* Projet Android
    * Point d’entrée (activité, service, récepteur)
    * Arguments et données intentionnels
* Projet iOS
    * Mode (Normal, Récupération en arrière-plan)
* Projet d’extension iOS
    * Application de démarrage : par défaut ou personnalisée
* Projet WatchKit
    * Mode (Coup d’œil, Notification)
    * Charge utile de la notification
