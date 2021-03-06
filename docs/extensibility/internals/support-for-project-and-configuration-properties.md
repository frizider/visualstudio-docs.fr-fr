---
title: "Prise en charge pour le projet et les propriétés de Configuration | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, suppporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
caps.latest.revision: "25"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1490c350a9c2c5fc91d516e2658c47a8246eb5d7
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="support-for-project-and-configuration-properties"></a>Prise en charge des propriétés de Configuration et de projet
Le **propriétés** fenêtre dans le [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] l’environnement de développement intégré (IDE) peut afficher les propriétés de configuration et de projet. Vous pouvez fournir une page de propriétés pour votre propre type de projet afin que l’utilisateur peut définir les propriétés de votre application.  
  
 En sélectionnant un nœud de projet dans **l’Explorateur de solutions** , puis en cliquant sur **propriétés** sur la **projet** menu, vous pouvez ouvrir une boîte de dialogue qui inclut le projet et la configuration Propriétés. Dans [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] et [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]et le projet types dérivés de ces langues, cette boîte de dialogue s’affiche comme une page à onglets dans le [général, environnement, boîte de dialogue Options](../../ide/reference/general-environment-options-dialog-box.md). Pour plus d’informations, consultez [pas dans la Build : procédure pas à pas : exposition d’un projet et les propriétés de Configuration (c#)](http://msdn.microsoft.com/en-us/d850d63b-25e2-4505-9f3d-eb038d7c1d0e).  
  
 Managed Package Framework pour les projets (MPFProj) fournit des classes d’assistance pour créer et gérer le nouveau système de projet. Vous pouvez trouver la source des instructions de code et la compilation à [MPF de projets - Visual Studio 2013](http://mpfproj12.codeplex.com/).  
  
## <a name="persistence-of-project-and-configuration-properties"></a>Persistance de projet et des propriétés de Configuration  
 Propriétés de configuration et de projet sont conservées dans un fichier projet qui a une extension de nom de fichier associé avec le type de projet, par exemple, .csproj, .vbproj et .myproj. Projets de langage utilisent généralement un fichier de modèle pour générer le fichier de projet. Toutefois, il existe réellement plusieurs manières pour associer des modèles et des types de projets. Pour plus d’informations, consultez [NIB : modèles Visual Studio](http://msdn.microsoft.com/en-us/141fccaa-d68f-4155-822b-27f35dd94041) et [Description du modèle active (. Fichiers VSDir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md).  
  
 Propriétés de configuration et de projet sont créées en ajoutant des éléments au fichier de modèle. Ces propriétés sont ensuite disponibles pour tout projet créé à l’aide du type de projet qui utilise ce modèle. [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]projets et le MPFProj utilisent tous deux le [pas dans la Build : vue d’ensemble de MSBuild](http://msdn.microsoft.com/en-us/b588fd73-a45b-4706-908f-cc131bccfbde) schéma des fichiers de modèle. Ces fichiers ont une section PropertyGroup pour chaque configuration. Propriétés de projets sont généralement conservées dans la première section PropertyGroup, ce qui a un argument de la Configuration définie sur une chaîne null.  
  
 Le code suivant illustre le début d’un fichier de projet MSBuild base.  
  
```  
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
    <Name>SomeProjectSix</Name>  
    <SchemaVersion>2.0</SchemaVersion>  
  </PropertyGroup>  
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
    <Optimize>false</Optimize>  
  </PropertyGroup>  
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">  
    <Optimize>true</Optimize>  
```  
  
 Dans ce fichier de projet, `<Name>` et `<SchemaVersion>` sont des propriétés du projet, et `<Optimize>` est une propriété de configuration.  
  
 Il est responsable de projet pour rendre persistantes les propriétés de projet et la configuration du fichier projet.  
  
> [!NOTE]
>  Un projet peut optimiser la persistance par des valeurs de propriété uniquement persistantes qui diffèrent de leurs valeurs par défaut.  
  
## <a name="support-for-project-and-configuration-properties"></a>Prise en charge des propriétés de Configuration et de projet  
 La `Microsoft.VisualStudio.Package.SettingsPage` classe implémente des pages de propriétés de projet et la configuration. L’implémentation par défaut de `SettingsPage` propose des propriétés publiques à un utilisateur dans une grille de propriétés génériques. Le `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` méthode sélectionne des classes dérivées de `SettingsPage` pour les grilles de propriétés de projet. Le `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` méthode sélectionne des classes dérivées de `SettingsPage` pour les grilles de propriétés de configuration. Votre projet doit substituer ces méthodes pour sélectionner les pages de propriétés appropriée.  
  
 Le `SettingsPage` classe et la `Microsoft.VisualStudio.Package.ProjectNode` classe offrent ces méthodes pour rendre persistantes les propriétés de configuration et de projet :  
  
-   `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty`et `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` conserver les propriétés du projet.  
  
-   `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty`et `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` conserver les propriétés de configuration.  
  
    > [!NOTE]
    >  Les implémentations de la `Microsoft.VisualStudio.Package.SettingsPage` et `Microsoft.VisualStudio.Package.ProjectNode` classes utilisent la `Microsoft.Build.BuildEngine` (MSBuild) des méthodes pour obtenir et définir les propriétés de configuration et de projet à partir du fichier projet.  
  
 La classe de dérivation `SettingsPage` doit implémenter `Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` et `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` pour conserver les propriétés de configuration du projet ou du fichier projet.  
  
## <a name="provideobjectattribute-and-registry-path"></a>ProvideObjectAttribute et le chemin d’accès du Registre  
 Les classes dérivées de `SettingsPage` sont conçus pour être partagés entre les VSPackages. Pour permettre à un VSPackage créer une classe dérivée de `SettingsPage`, ajoutez un `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` à une classe dérivée de `Microsoft.VisualStudio.Shell.Package`.  
  
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_1.cs)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_1.vb)]  
  
 Le VSPackage à laquelle l’attribut est attaché est sans important. Quand un VSPackage est enregistré avec [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], l’id de classe (CLSID) de tout objet qui peut être créé est enregistré afin qu’un appel à <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> pouvez la créer.  
  
 Le chemin d’accès du Registre d’un objet qui peut être créé est déterminée en combinant <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>, le mot, CLSID et le guid du type d’objet. Si `MyProjectPropertyPage` classe a un guid de {3c693da2-5bca-49b3-bd95-ffe0a39dd723} et le UserRegistryRoot est HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, le chemin d’accès du Registre serait HKEY_CURRENT_USER\Software\Microsoft\VisualStudio \8.0Exp\CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39dd723}.  
  
## <a name="project-and-configuration-property-attributes-and-layout"></a>Projet et les attributs de propriété de Configuration et la disposition  
 Le <xref:System.ComponentModel.CategoryAttribute>, <xref:System.ComponentModel.DisplayNameAttribute>, et <xref:System.ComponentModel.DescriptionAttribute> attributs déterminent la mise en page, l’étiquetage et la description des propriétés de projet et de configuration dans une page de propriétés génériques. Ces attributs déterminent la catégorie, nom complet et la description de l’option, respectivement.  
  
> [!NOTE]
>  Attributs équivalents, SRCategory, LocDisplayName et SRDescription, utilisez les ressources de chaîne pour la localisation et sont définies dans [MPF de projets - Visual Studio 2013](http://mpfproj12.codeplex.com/).  
  
 Prenons le fragment de code suivant :  
  
 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_2.vb)]
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_2.cs)]  
  
 Le `MyConfigProp` propriété configuration apparaît dans la page de propriété de configuration en tant que **mes Config propriété** dans la catégorie, **catégorie Mes**. Si l’option est sélectionnée, la description, **ma Description**, apparaît dans le volet de description.  
  
## <a name="see-also"></a>Voir aussi  
 [Ajout et suppression de Pages de propriétés](../../extensibility/adding-and-removing-property-pages.md)   
 [Projets](../../extensibility/internals/projects.md)   
 [Fichiers de description de répertoire de modèles (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)