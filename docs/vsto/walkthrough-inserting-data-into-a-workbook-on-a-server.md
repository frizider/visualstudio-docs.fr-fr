---
title: "Procédure pas à pas : Insertion de données dans un classeur sur un serveur | Documents Microsoft"
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
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
- workbooks [Office development in Visual Studio], inserting data
ms.assetid: e6481902-781c-4666-bc18-4d69368c9bb3
caps.latest.revision: "38"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ca768bd681c20826ffbdeeec94706b8b37c129f3
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="walkthrough-inserting-data-into-a-workbook-on-a-server"></a>Procédure pas à pas : insertion de données dans un classeur sur un serveur
  Cette procédure pas à pas montre comment insérer des données dans un jeu de données est mise en cache dans un classeur Microsoft Office Excel sans démarrer Excel à l’aide de la <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Cette procédure pas à pas décrit les tâches suivantes :  
  
-   Définition d’un dataset qui contient les données à partir de la base de données AdventureWorksLT.  
  
-   Création d’instances du jeu de données dans un projet de classeur Excel et un projet d’application console.  
  
-   Création d’un <xref:Microsoft.Office.Tools.Excel.ListObject> qui est lié au jeu de données dans le classeur.  
  
-   Ajout du jeu de données dans le classeur dans le cache de données.  
  
-   Insertion de données dans le dataset mis en cache en exécutant le code dans l’application console, sans démarrer Excel.  
  
 Bien que cette procédure pas à pas suppose que vous exécutez le code sur votre ordinateur de développement, le code illustré dans cette procédure pas à pas peut être utilisé sur un serveur qui n’ont pas installé Excel.  
  
> [!NOTE]  
>  Il est possible que pour certains des éléments de l'interface utilisateur de Visual Studio, votre ordinateur affiche des noms ou des emplacements différents de ceux indiqués dans les instructions suivantes. L'édition de Visual Studio dont vous disposez et les paramètres que vous utilisez déterminent ces éléments. Pour plus d’informations, consultez [Personnaliser l’IDE Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Conditions préalables  
 Pour exécuter cette procédure pas à pas, vous devez disposer des composants suivants :  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Accès à une instance en cours d’exécution de Microsoft SQL Server ou Microsoft SQL Server Express à laquelle la base de données AdventureWorksLT exemple lui. Vous pouvez télécharger la base de données AdventureWorksLT à partir de la [site CodePlex Web](http://go.microsoft.com/fwlink/?linkid=87843). Pour plus d’informations sur l’attachement d’une base de données, consultez les rubriques suivantes :  
  
    -   Pour attacher une base de données à l’aide de SQL Server Management Studio ou de SQL Server Management Studio Express, consultez [Comment : attacher une base de données (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/b4efb0ae-cfe6-4d81-a4b4-6e4916885caa).  
  
    -   Pour attacher une base de données à l’aide de la ligne de commande, consultez [Comment : attacher un fichier de base de données à SQL Server Express](http://msdn.microsoft.com/en-us/0f8e42b5-7a8c-4c30-8c98-7d2bdc8dcc68).  
  
## <a name="creating-a-class-library-project-that-defines-a-dataset"></a>Création d’un projet de bibliothèque de classes qui définit un jeu de données  
 Pour utiliser le même jeu de données dans un projet de classeur Excel et une application console, vous devez définir le jeu de données dans un assembly distinct qui est référencé par ces deux projets. Pour cette procédure pas à pas, définissez le jeu de données dans un projet de bibliothèque de classes.  
  
#### <a name="to-create-the-class-library-project"></a>Pour créer le projet de bibliothèque de classes  
  
1.  Démarrez [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Dans le menu **Fichier** , pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
3.  Dans le volet Modèles, développez **Visual C#** ou **Visual Basic**, puis cliquez sur **Windows**.  
  
4.  Dans la liste des modèles de projet, sélectionnez **bibliothèque de classes**.  
  
5.  Dans le **nom** , tapez **AdventureWorksDataSet**.  
  
6.  Cliquez sur **Parcourir**, accédez à votre %UserProfile%\My Documents (Windows XP ou version antérieure) ou le dossier %UserProfile%\Documents (pour Windows Vista), puis cliquez sur **sélectionner le dossier**.  
  
7.  Dans le **nouveau projet** boîte de dialogue zone, vérifiez que le **créer le répertoire pour la solution** case à cocher n’est pas activée.  
  
8.  Cliquez sur **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Ajoute le **AdventureWorksDataSet** projet **l’Explorateur de solutions** et ouvre le **Class1.cs** ou **Class1.vb** fichier de code.  
  
9. Dans **l’Explorateur de solutions**, avec le bouton droit **Class1.cs** ou **Class1.vb**, puis cliquez sur **supprimer**. Il est inutile ce fichier pour cette procédure pas à pas.  
  
## <a name="defining-a-dataset-in-the-class-library-project"></a>Définition d’un Dataset dans le projet de bibliothèque de classes  
 Définissez un dataset typé qui contient les données à partir de la base de données AdventureWorksLT pour SQL Server 2005. Plus loin dans cette procédure pas à pas, vous ferez référence ce jeu de données à partir d’un projet de classeur Excel et un projet d’application console.  
  
 Le jeu de données est un *dataset typé* qui représente les données dans la table Product de la base de données AdventureWorksLT. Pour plus d’informations sur les datasets typés, consultez [outils Dataset dans Visual Studio](/visualstudio/data-tools/dataset-tools-in-visual-studio).  
  
#### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>Pour définir un dataset typé dans le projet de bibliothèque de classes  
  
1.  Dans **l’Explorateur de solutions**, cliquez sur le **AdventureWorksDataSet** projet.  
  
2.  Si la fenêtre **Sources de données** n'est pas visible, affichez-la en choisissant, dans la barre de menus, **Affichage**, **Autres fenêtres**, **Sources de données**.  
  
3.  Choisissez **Ajouter une nouvelle source de données** pour démarrer l' **Assistant Configuration de source de données**.  
  
4.  Cliquez sur **Base de données**, puis sur **Suivant**.  
  
5.  Si vous avez une connexion existante à la base de données AdventureWorksLT, choisissez cette connexion, puis cliquez sur **suivant**.  
  
     Sinon, cliquez sur **Nouvelle connexion**et utilisez la boîte de dialogue **Ajouter une connexion** pour créer la connexion. Pour plus d’informations, consultez [Comment : se connecter à des données dans une base de données](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md).  
  
6.  Dans la page **Enregistrer la chaîne de connexion dans le fichier de configuration de l’application** , cliquez sur **Suivant**.  
  
7.  Dans le **choisir vos objets de base de données** page, développez **Tables** et sélectionnez **Product (SalesLT)**.  
  
8.  Cliquez sur **Terminer**.  
  
     Le fichier AdventureWorksLTDataSet.xsd est ajouté à la **AdventureWorksDataSet** projet. Ce fichier définit les éléments suivants :  
  
    -   Un dataset typé nommé `AdventureWorksLTDataSet`. Ce jeu de données représente le contenu de la table Product dans la base de données AdventureWorksLT.  
  
    -   Un TableAdapter nommé `ProductTableAdapter`. Ce TableAdapter peut être utilisé pour lire et écrire des données le `AdventureWorksLTDataSet`. Pour plus d'informations, consultez [TableAdapter Overview](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).  
  
     Vous utiliserez ces deux objets ultérieurement dans cette procédure pas à pas.  
  
9. Dans **l’Explorateur de solutions**, avec le bouton droit **AdventureWorksDataSet** et cliquez sur **Build**.  
  
     Vérifiez que le projet se génère sans erreur.  
  
## <a name="creating-an-excel-workbook-project"></a>Création d'un projet de classeur Excel  
 Créer un projet de classeur Excel pour l’interface aux données. Plus loin dans cette procédure pas à pas, vous allez créer un <xref:Microsoft.Office.Tools.Excel.ListObject> qui affiche les données, et vous allez ajouter une instance du jeu de données dans le cache de données dans le classeur.  
  
#### <a name="to-create-the-excel-workbook-project"></a>Pour créer le projet de classeur Excel  
  
1.  Dans **l’Explorateur de solutions**, avec le bouton droit le **AdventureWorksDataSet** solution, pointez sur **ajouter**, puis cliquez sur **nouveau projet**.  
  
2.  Dans le volet Modèles, développez **Visual C#** ou **Visual Basic**, puis développez **Office/SharePoint**.  
  
3.  Sous le nœud développé **Office/SharePoint** , sélectionnez le nœud **Compléments Office** .  
  
4.  Dans la liste des modèles de projet, sélectionnez le projet **Classeur Excel 2010** ou **Classeur Excel 2013** .  
  
5.  Dans le **nom** , tapez **AdventureWorksReport**. Ne modifiez pas l’emplacement.  
  
6.  Cliquez sur **OK**.  
  
     L' **Assistant Projet Visual Studio Tools pour Office** s'ouvre.  
  
7.  Vérifiez que **créer un nouveau document** est sélectionné, puis cliquez sur **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Ouvre le **AdventureWorksReport** classeur dans le concepteur et ajoute le **AdventureWorksReport** projet **l’Explorateur de solutions**.  
  
## <a name="adding-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Ajout du jeu de données à des Sources de données dans le projet de classeur Excel  
 Avant de pouvoir afficher le jeu de données dans le classeur Excel, vous devez d’abord ajouter le jeu de données à des sources de données dans le projet de classeur Excel.  
  
#### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>Pour ajouter le jeu de données aux sources de données dans le projet de classeur Excel  
  
1.  Dans **l’Explorateur de solutions**, double-cliquez sur **Sheet1.cs** ou **Sheet1.vb** sous le **AdventureWorksReport** projet.  
  
     Le classeur s’ouvre dans le concepteur.  
  
2.  Dans le menu **Données** , cliquez sur **Ajouter une nouvelle source de données**.  
  
     Le **Assistant de Configuration de Source de données** s’ouvre.  
  
3.  Cliquez sur **objet**, puis cliquez sur **suivant**.  
  
4.  Dans le **sélectionnez l’objet que vous souhaitez lier** à la page, cliquez sur **ajouter une référence**.  
  
5.  Sur le **projets** , cliquez sur **AdventureWorksDataSet** puis cliquez sur **OK**.  
  
6.  Sous le **AdventureWorksDataSet** espace de noms de la **AdventureWorksDataSet** assembly, cliquez sur **AdventureWorksLTDataSet** puis cliquez sur **terminer** .  
  
     Le **des Sources de données** fenêtre s’ouvre, et **AdventureWorksLTDataSet** est ajouté à la liste des sources de données.  
  
## <a name="creating-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>Création d’un contrôle ListObject lié à une Instance du jeu de données  
 Pour afficher le jeu de données dans le classeur, créez un <xref:Microsoft.Office.Tools.Excel.ListObject> qui est lié à une instance du jeu de données. Pour plus d’informations sur la liaison des contrôles aux données, consultez [Binding Data to Controls in Office Solutions](../vsto/binding-data-to-controls-in-office-solutions.md).  
  
#### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>Pour créer un ListObject lié à une instance du jeu de données  
  
1.  Dans le **des Sources de données** fenêtre, développez le **AdventureWorksLTDataSet** nœud sous **AdventureWorksDataSet**.  
  
2.  Sélectionnez le **produit** nœud, cliquez sur la flèche déroulante qui s’affiche, sélectionnez **ListObject** dans la liste déroulante.  
  
     Si la flèche de déroulement n’apparaît pas, vérifiez que le classeur est ouvert dans le concepteur.  
  
3.  Faites glisser le **produit** table à la cellule A1.  
  
     A <xref:Microsoft.Office.Tools.Excel.ListObject> contrôle nommé `productListObject` est créé sur la feuille de calcul, en commençant par la cellule A1. En même temps, un objet dataset nommé `adventureWorksLTDataSet` et un <xref:System.Windows.Forms.BindingSource> nommé `productBindingSource` sont ajoutés au projet. <xref:Microsoft.Office.Tools.Excel.ListObject> est lié à <xref:System.Windows.Forms.BindingSource>, qui est lui-même lié à l’objet dataset.  
  
## <a name="adding-the-dataset-to-the-data-cache"></a>Ajout du jeu de données dans le Cache de données  
 Pour permettre au code en dehors du projet de classeur Excel pour accéder au dataset dans le classeur, vous devez ajouter le jeu de données dans le cache de données. Pour plus d’informations sur le cache de données, consultez [mis en cache les données dans les personnalisations au niveau du Document](../vsto/cached-data-in-document-level-customizations.md) et [mise en cache des données](../vsto/caching-data.md).  
  
#### <a name="to-add-the-dataset-to-the-data-cache"></a>Pour ajouter le jeu de données dans le cache de données  
  
1.  Dans le concepteur, cliquez sur **adventureWorksLTDataSet**.  
  
2.  Dans le **propriétés** , configurez la **modificateurs** propriété **Public**.  
  
3.  Définir le **CacheInDocument** propriété **True**.  
  
## <a name="checkpoint"></a>Point de contrôle  
 Générez et exécutez le projet de classeur Excel pour vous assurer qu’il se compile et s’exécute sans erreur.  
  
#### <a name="to-build-and-run-the-project"></a>Pour générer et exécuter le projet  
  
1.  Dans **l’Explorateur de solutions**, avec le bouton droit le **AdventureWorksReport** de projet, choisissez **déboguer**, puis cliquez sur **démarrer une nouvelle instance**.  
  
     Le projet est généré et le classeur s’ouvre dans Excel. Le <xref:Microsoft.Office.Tools.Excel.ListObject> dans **Feuil1** est vide, car le `adventureWorksLTDataSet` objet dans le cache de données n’a encore aucune donnée. Dans la section suivante, vous allez utiliser une application console pour remplir le `adventureWorksLTDataSet` objet avec les données.  
  
2.  Fermez Excel. Ne pas enregistrer les modifications.  
  
## <a name="creating-a-console-application-project"></a>Création d’un projet d’Application Console  
 Créez un projet d’application console à utiliser pour insérer des données dans le dataset mis en cache dans le classeur.  
  
#### <a name="to-create-the-console-application-project"></a>Pour créer le projet d’application console  
  
1.  Dans **l’Explorateur de solutions**, avec le bouton droit le **AdventureWorksDataSet** solution, pointez sur **ajouter**, puis cliquez sur **nouveau projet**.  
  
2.  Dans le **Types de projets** volet, développez **Visual C#** ou **Visual Basic**, puis cliquez sur **Windows**.  
  
3.  Dans le **modèles** volet, sélectionnez **Application Console**.  
  
4.  Dans le **nom** , tapez **DataWriter**. Ne modifiez pas l’emplacement.  
  
5.  Cliquez sur **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Ajoute le **DataWriter** projet **l’Explorateur de solutions** et ouvre le **Program.cs** ou **Module1.vb** fichier de code.  
  
## <a name="adding-data-to-the-cached-dataset-by-using-the-console-application"></a>Ajout de données pour le Dataset mis en cache à l’aide de l’Application Console  
 Utilisez la <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe dans l’application console pour remplir le dataset mis en cache dans le classeur avec les données.  
  
#### <a name="to-add-data-to-the-cached-dataset"></a>Pour ajouter des données pour le dataset mis en cache  
  
1.  Dans **l’Explorateur de solutions**, avec le bouton droit le **DataWriter** projet puis cliquez sur **ajouter une référence**.  
  
2.  Sur le **.NET** onglet, sélectionnez **Microsoft.VisualStudio.Tools.Applications.ServerDocument**.  
  
3.  Cliquez sur **OK**.  
  
4.  Dans **l’Explorateur de solutions**, avec le bouton droit le **DataWriter** projet puis cliquez sur **ajouter une référence**.  
  
5.  Sur le **projets** onglet, sélectionnez **AdventureWorksDataSet**, puis cliquez sur **OK**.  
  
6.  Ouvrez le fichier Program.cs ou Module1.vb dans l’éditeur de Code.  
  
7.  Ajoutez le code suivant **à l’aide de** (pour c#) ou **importations** (pour Visual Basic) en haut du fichier de code.  
  
     [!code-csharp[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#1)]
     [!code-vb[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#1)]  
  
8.  Ajoutez le code suivant à la méthode `Main` . Ce code déclare les objets suivants :  
  
    -   Instances de la `AdventureWorksLTDataSet` et `ProductTableAdapter` types qui sont définis dans le **AdventureWorksDataSet** projet.  
  
    -   Le chemin d’accès au classeur AdventureWorksReport dans le dossier de génération de la **AdventureWorksReport** projet.  
  
    -   A <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> objet à utiliser pour accéder au cache de données dans le classeur.  
  
        > [!NOTE]  
        >  Le code suivant suppose que vous utilisez un classeur qui a l’extension de fichier .xlsx. Si le classeur dans votre projet a une extension de fichier différent, modifiez le chemin d’accès si nécessaire.  
  
     [!code-csharp[Trin_CachedDataWalkthroughs#3](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#3)]
     [!code-vb[Trin_CachedDataWalkthroughs#3](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#3)]  
  
9. Ajoutez le code suivant à la `Main` (méthode), après le code que vous avez ajouté à l’étape précédente. Ce code exécute les tâches suivantes :  
  
    -   Il remplit l’objet dataset typé à l’aide de l’adaptateur de table.  
  
    -   Elle utilise le <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> propriété de la <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe pour accéder au dataset mis en cache dans le classeur.  
  
    -   Elle utilise le <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> méthode pour remplir le dataset mis en cache avec les données du dataset typé local.  
  
     [!code-csharp[Trin_CachedDataWalkthroughs#4](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#4)]
     [!code-vb[Trin_CachedDataWalkthroughs#4](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#4)]  
  
10. Dans **l’Explorateur de solutions**, avec le bouton droit le **DataWriter** de projet, pointez sur **déboguer**, puis cliquez sur **démarrer une nouvelle instance**.  
  
     Le projet est généré, et l’application console affiche plusieurs messages d’état lorsque le jeu de données local est rempli et lorsque l’application enregistre les données dans le dataset mis en cache dans le classeur. Appuyez sur ENTRÉE pour fermer l’application.  
  
## <a name="testing-the-workbook"></a>Test du classeur  
 Lorsque vous ouvrez le classeur, la <xref:Microsoft.Office.Tools.Excel.ListObject> affiche maintenant les données qui a été ajoutées au jeu de données mises en cache à l’aide de l’application console.  
  
#### <a name="to-test-the-workbook"></a>Pour tester le classeur  
  
1.  Fermez le classeur AdventureWorksReport dans le concepteur Visual Studio, s’il est toujours ouvert.  
  
2.  Dans l’Explorateur de fichiers, ouvrez le classeur AdventureWorksReport dans le dossier de génération de la **AdventureWorksReport** projet. Par défaut, le dossier de génération est dans un des emplacements suivants :  
  
    -   %USERPROFILE%\My Documents\AdventureWorksReport\bin\Debug (pour Windows XP ou version antérieure)  
  
    -   %USERPROFILE%\Documents\AdventureWorksReport\bin\Debug (pour Windows Vista)  
  
3.  Vérifiez que le <xref:Microsoft.Office.Tools.Excel.ListObject> est remplie avec les données une fois que vous ouvrez le classeur.  
  
## <a name="next-steps"></a>Étapes suivantes  
 Pour plus d’informations sur l’utilisation des données mises en cache à partir de ces rubriques :  
  
-   Modifiez les données dans un dataset mis en cache sans démarrer Excel. Pour plus d’informations, consultez [procédure pas à pas : modification des données mises en cache dans un classeur sur un serveur](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Procédure pas à pas : Modification des données mises en cache dans un classeur sur un serveur](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)   
 [Connexion à des données dans des applications Windows Forms](/visualstudio/data-tools/connecting-to-data-in-windows-forms-applications)  
  
  