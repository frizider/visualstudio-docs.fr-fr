---
title: "Présentation du développement de Solutions Office (VSTO) | Documents Microsoft"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies, Office
- Office development in Visual Studio, about developing solutions
ms.assetid: 5dfc519f-a851-4661-8d2b-47e0d221e10e
caps.latest.revision: "69"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1c35be3e79aea37b82e9ae46463582a0874e51a4
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="office-solutions-development-overview-vsto"></a>Vue d’ensemble du développement des solutions Office (VSTO)
  En utilisant Microsoft Office comme partie frontale des solutions, vous pouvez tirer parti des interfaces utilisateur et outils Microsoft Office familiers tels que les fonctionnalités de traitement de texte dans Word, les fonctionnalités d'analyse des données d'Excel et les fonctionnalités de gestion de la messagerie électronique d'Outlook. Vous pouvez développer des solutions dans Visual Studio pour personnaliser des applications Office et ajouter les fonctionnalités spécifiques dont vous avez besoin pour vos processus métier. Par exemple, vous pouvez transformer Word en générateur de contrats qui assemble des contrats à partir de parties préexistantes qui peuvent être modifiables ou non. Avec Excel, vous pouvez créer une feuille de calcul de budget automatisée personnalisée pour différents projets. Vos utilisateurs peuvent aussi mettre des solutions Office hors connexion, ce qui permet de rendre des solutions complexes plus pratiques qu'elles ne le seraient en utilisant une architecture basée sur le Web.  
  
 Cette rubrique fournit une vue d'ensemble des types de solutions Office que vous pouvez créer à l'aide des modèles Visual Studio Tools pour Office (VSTO) disponibles dans les Outils de développement Office dans Visual Studio. Pour obtenir des informations générales sur le développement avec Office, consultez le [Centre de développement Office](https://dev.office.com/).  
  
## <a name="choosing-an-office-project-type"></a>Choix d'un type de projet Office  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fournit les types suivants de modèles de projet pour le développement de solutions Office basées sur VSTO :  
  
-   Les**personnalisations au niveau du document** sont associées à un document spécifique.  
  
-   Les**VSTO Add-ins** sont associés à l'application elle-même.  
  
 Pour choisir le type de projet le mieux adapté à votre solution, déterminez si vous souhaitez que votre code s'exécute uniquement quand un document spécifique est ouvert ou si vous souhaitez que le code soit disponible à chaque exécution de l'application. Pour plus d’informations sur les modèles de projet, consultez [vue d’ensemble des modèles de projet Office](../vsto/office-project-templates-overview.md).  
  
 Les types de projets que vous pouvez créer dépendent des applications Office installées sur l'ordinateur de développement. Pour plus d'informations, consultez [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md).  
  
### <a name="document-level-customizations"></a>Personnalisations au niveau du document  
 Les personnalisations au niveau du document se composent d'un assembly associé à un document, classeur ou modèle unique dans Microsoft Office Word ou Microsoft Office Excel. L'assembly est chargé quand le document associé est ouvert. Les fonctionnalités des personnalisations que vous créez sont disponibles uniquement quand le document associé est ouvert. Les personnalisations ne peuvent pas apporter de modifications au niveau de l'application, comme l'affichage d'un nouvel élément de menu ou onglet de ruban quand un document est ouvert.  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] inclut des outils pour vous aider à créer des personnalisations au niveau du document. Le document que vous personnalisez est hébergé comme une aire de conception dans [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], ce qui permet de concevoir le document par glisser-déplacer de contrôles. De nombreuses autres fonctionnalités [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sont disponibles dans les projets au niveau du document, tels que les contrôles Windows Forms, les liaisons de données par glisser-déplacer et un débogueur intégré.  
  
 Pour plus d'informations sur les personnalisations, consultez les rubriques suivantes :  
  
-   [Bien démarrer avec la programmation des personnalisations au niveau du document pour Excel](../vsto/getting-started-programming-document-level-customizations-for-excel.md)  
  
-   [Bien démarrer avec la programmation des personnalisations au niveau du document pour Word](../vsto/getting-started-programming-document-level-customizations-for-word.md)  
  
-   [Architecture des personnalisations au niveau du document](../vsto/architecture-of-document-level-customizations.md)  
  
### <a name="vsto-add-ins"></a>VSTO Add-ins  
 Les compléments VSTO sont constitués d'un assembly associé à une application Microsoft Office. En général, le complément VSTO est exécuté au démarrage de l’application associée, bien que les utilisateurs puissent également charger des compléments VSTO quand l’application est en cours d’exécution. Les fonctionnalités des compléments VSTO que vous créez sont accessibles à l’application, quels que soient les documents ouverts.  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] inclut des outils pour vous aider à créer des compléments VSTO. Les projets de complément incluent une classe générée automatiquement qui représente le complément VSTO. Cette classe fournit des propriétés et événements que vous pouvez utiliser pour accéder au modèle objet de l’application hôte et exécuter du code quand le complément VSTO est chargé et arrêté. De nombreuses autres fonctionnalités [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sont disponibles dans les projets de complément VSTO, comme Windows Forms et un débogueur intégré.  
  
 Pour plus d’informations sur les compléments VSTO, consultez les rubriques suivantes :  
  
-   [Bien démarrer avec la programmation des compléments VSTO](../vsto/getting-started-programming-vsto-add-ins.md)  
  
-   [Architecture des compléments VSTO](../vsto/architecture-of-vsto-add-ins.md)  
  
## <a name="automating-office-applications-by-using-primary-interop-assemblies"></a>Automatisation d'applications Office à l'aide d'assemblys PIA (Primary Interop Assemblies)  
 Vous pouvez incorporer par programme les fonctionnalités d'une application Office dans votre solution en écrivant du code qui accède au modèle objet de l'application. Les modèles objet sont une organisation de classes qui exposent des fonctionnalités via diverses propriétés et méthodes. Le modèle objet est différent pour chaque application Office.  
  
 Pour utiliser le modèle objet d'une application Office à partir d'une solution créée à l'aide des Outils de développement Office dans [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], vous devez utiliser l'assembly PIA pour l'application. L'assembly PIA permet au code managé dans votre solution d'interagir avec le modèle objet COM de l'application Office.  
  
 Pour que vous puissiez effectuer la plupart des tâches de développement, les assemblys PIA d'Office doivent être installés et inscrits dans le Global Assembly Cache de votre ordinateur de développement. Pour plus d'informations, consultez [Configuring a Computer to Develop Office Solutions](../vsto/configuring-a-computer-to-develop-office-solutions.md). Les assemblys PIA d'Office ne sont pas requis sur les ordinateurs des utilisateurs finaux pour l'exécution des solutions Office VSTO. Pour plus d'informations, consultez [Designing and Creating Office Solutions](../vsto/designing-and-creating-office-solutions.md).  
  
 Pour plus d'informations sur l'utilisation d'assemblys PIA dans les solutions Office VSTO, consultez les rubriques suivantes :  
  
-   [Écriture de code dans les solutions Office](../vsto/writing-code-in-office-solutions.md)  
  
-   [Assemblys PIA (Primary Interop Assembly) Office](../vsto/office-primary-interop-assemblies.md)  
  
## <a name="running-microsoft-vsto-office-solutions-on-end-user-computers"></a>Exécution de solutions Microsoft Office VSTO sur les ordinateurs des utilisateurs finaux  
 Quand vous créez une solution Office VSTO, vous devez réfléchir à la façon dont les spécifications de déploiement peuvent affecter vos choix de développement.  
  
### <a name="deployment-options"></a>Options de déploiement  
 Utilisez ClickOnce ou Windows Installer pour déployer les solutions que vous créez à l'aide des Outils de développement Office de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Le déploiement ClickOnce vous permet de créer des solutions à mise à jour automatique qui peuvent être installées et exécutées avec une intervention minimale de l'utilisateur. Les fichiers Windows Installer (.msi) peuvent être distribués facilement aux ordinateurs des utilisateurs finaux ou distribués à l'aide de Systems Management Server (SMS). Pour plus d’informations sur le déploiement de solutions Office VSTO, consultez [déploiement d’une Solution Office](../vsto/deploying-an-office-solution.md).  
  
### <a name="installing-prerequisites"></a>Installation des composants requis  
 Avant que les utilisateurs finaux ne puissent exécuter une solution créée à l'aide des Outils de développement Office de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], certains composants doivent être installés sur leur ordinateur. Si vous déployez votre solution en utilisant ClickOnce ou en créant un fichier Windows Installer, ces composants requis peuvent être installés avec votre solution. Pour plus d’informations, consultez [Composants requis pour les solutions Office en vue du déploiement](http://msdn.microsoft.com/en-us/9f672809-43a3-40a1-9057-397ce3b5126e) et [Comment : installer les composants requis sur les ordinateurs des utilisateurs finaux pour exécuter des solutions Office](http://msdn.microsoft.com/en-us/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98).  
  
### <a name="security"></a>Sécurité  
 La sécurité pour les solutions Office VSTO est appliquée par une série de contrôles effectués par [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] au moment de l'installation et du chargement de la solution. Ces contrôles permettent notamment de vérifier si l'emplacement du manifeste de déploiement ou le certificat utilisé pour signer le manifeste est approuvé. Pour plus d'informations, consultez [Securing Office Solutions](../vsto/securing-office-solutions.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Mise en route &#40; développement Office dans Visual Studio &#41;](../vsto/getting-started-office-development-in-visual-studio.md)   
 [Architecture des personnalisations au niveau du Document](../vsto/architecture-of-document-level-customizations.md)   
 [Architecture des Compléments VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Prise en main de programmation des personnalisations au niveau du Document pour Excel](../vsto/getting-started-programming-document-level-customizations-for-excel.md)   
 [Prise en main de programmation des personnalisations au niveau du Document pour Word](../vsto/getting-started-programming-document-level-customizations-for-word.md)   
 [Bien démarrer avec la programmation des compléments VSTO](../vsto/getting-started-programming-vsto-add-ins.md)  
  
  