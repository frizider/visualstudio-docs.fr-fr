---
title: "ProjectSubType, élément (modèles Visual Studio) | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
caps.latest.revision: "13"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c42cfdd72207fdca7fbbe0b17b0f96f20066f098
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="projectsubtype-element-visual-studio-templates"></a>ProjectSubType, élément (modèles Visual Studio)
Classe le modèle dans une sous-catégorie de la valeur spécifiée dans le `ProjectType` élément.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<ProjectSubType >  
  
## <a name="syntax"></a>Syntaxe  
  
```  
<ProjectSubType> SubType </ProjectSubType>  
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
 Aucun  
  
### <a name="child-elements"></a>Éléments enfants  
 Aucun.  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Élément requis.<br /><br /> Définit la catégorie du modèle et comment il s’affiche dans la boîte de dialogue **Nouveau projet** ou **Ajouter un nouvel élément** .|  
  
## <a name="text-value"></a>Valeur texte  
 Une valeur texte est requise.  
  
 Cette valeur spécifie la sous-catégorie du modèle.  
  
## <a name="remarks"></a>Remarques  
 `ProjectSubType` est un élément enfant facultatif de `TemplateData`.  
  
 Le `ProjectSubType` élément fournit une sous-catégorie à la [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) élément. Cette valeur peut inclure :  
  
-   `SmartDevice-NETCFv1`: Spécifie que le modèle concerne la [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] version 1.0.  
  
-   `SmartDevice-NETCFv2`: Spécifie que le modèle concerne la [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] version 2.0.  
  
 Si un modèle contient un `ProjectType` élément avec la valeur `Web`, le `ProjectSubType` élément spécifie le langage de programmation du modèle. Cet élément peut avoir les valeurs suivantes :  
  
-   `CSharp`: Spécifie que le modèle crée un [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] projet Web ou un élément.  
  
-   `VisualBasic`: Spécifie que le modèle crée un [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] projet Web ou un élément.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant affiche les métadonnées d’un modèle de projet pour un [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] appareil ciblage de l’application le [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] version 2.0.  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic device template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <ProjectSubType>SmartDevice-NETCFv2</ProjectSubType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyTemplate.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>  
            <ProjectItem>Properties\Resources.resx</ProjectItem>  
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>  
            <ProjectItem>Properties\Settings.settings</ProjectItem>  
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Référence du schéma de modèle Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Création de modèles de projet et d’élément](../ide/creating-project-and-item-templates.md)   
 [Élément ProjectType (modèles Visual Studio)](../extensibility/projecttype-element-visual-studio-templates.md)