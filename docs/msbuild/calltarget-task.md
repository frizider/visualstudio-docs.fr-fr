---
title: "CallTarget, tâche | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CallTarget task [MSBuild]
- MSBuild, CallTarget task
ms.assetid: bb1fe2c4-4383-436f-8326-c24cc4a46150
caps.latest.revision: "6"
author: kempb
ms.author: kempb
manager: ghogen
ms.openlocfilehash: e88638d83a0d5920727e531f7101d4230abcce7c
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="calltarget-task"></a>CallTarget, tâche
Appelle les cibles spécifiées dans le fichier projet.  
  
## <a name="task-parameters"></a>Paramètres de tâche  
 Le tableau ci-dessous décrit les paramètres de la tâche `CallTarget`.  
  
|Paramètre|Description|  
|---------------|-----------------|  
|`RunEachTargetSeparately`|Paramètre de sortie `Boolean` facultatif.<br /><br /> Si `true`, le moteur [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] est appelé une fois pour chaque cible. Si `false`, le moteur [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] est appelé une fois pour générer toutes les cibles. La valeur par défaut est `false`.|  
|`TargetOutputs`|Paramètre de sortie <xref:Microsoft.Build.Framework.ITaskItem>`[]` facultatif.<br /><br /> Contient la sortie de toutes les cibles générées.|  
|`Targets`|Paramètre `String[]` facultatif.<br /><br /> Spécifie la ou les cibles à générer.|  
|`UseResultsCache`|Paramètre `Boolean` facultatif.<br /><br /> Si `true`, le résultat mis en cache est retourné, le cas échéant.<br /><br /> **Remarque** Si une tâche MSBuild est exécutée, son résultat est mis en cache dans une portée (ProjectFileName, GlobalProperties)[TargetNames] sous la forme d’une liste d’éléments de build.|  
  
## <a name="remarks"></a>Remarques  
 Si une cible spécifiée dans `Targets` échoue, et si `RunEachTargetSeparately` est `true`, la tâche continue à générer les cibles restantes.  
  
 Si vous souhaitez générer les cibles par défaut, utilisez la [tâche MSBuild](../msbuild/msbuild-task.md) et définissez le paramètre `Projects` sur la valeur `$(MSBuildProjectFile)`.  
  
 En plus des paramètres énumérés ci-dessus, cette tâche hérite des paramètres de la classe <xref:Microsoft.Build.Tasks.TaskExtension>, qui elle-même hérite de la classe <xref:Microsoft.Build.Utilities.Task>. Pour obtenir la liste de ces paramètres supplémentaires et leurs descriptions, consultez [Classe de base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemple  
 L’exemple suivant appelle `TargetA` à partir de `CallOtherTargets`.  
  
```xml  
<Project DefaultTargets="CallOtherTargets"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <Target Name="CallOtherTargets">  
        <CallTarget Targets="TargetA"/>  
    </Target>  
  
    <Target Name="TargetA">  
        <Message Text="Building TargetA..." />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Informations de référence sur les tâches](../msbuild/msbuild-task-reference.md)   
 [Cibles](../msbuild/msbuild-targets.md)