---
title: Attributs de prise en charge de Site Web | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: dba1aeb8f8e3ad368f050ef425f76cc6c94f99e8
ms.lasthandoff: 02/22/2017

---
# <a name="web-site-support-attributes"></a>Attributs de prise en charge de Site Web
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Projet de site Web peut être étendu pour prendre en charge pour le Web, langages de programmation. La langue doit s’inscrire avec [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] afin que les modèles de projet s’affiche dans le **nouveau Site Web** boîte de dialogue lorsque la langue est sélectionnée.  
  
 L’exemple de IronPython Studio inclut la prise en charge du site web. Vous pouvez le trouver avec le [VSSDK exemples](../../misc/vssdk-samples.md). Il inclut les classes d’attribut suivantes pour inscrire IronPython comme un langage de code-behind pour les nouveaux projets Web.  
  
## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute  
 Cet attribut est placé sur le projet de langage. Il ajoute la langue à la liste des langages de programmation Web de la **langage** liste dans le **nouveau Site Web** boîte de dialogue. Par exemple, la commande suivante ajoute IronPython à la liste :  
  
```  
[WebSiteProject("IronPython", "Iron Python")]public class PythonProjectPackage : ProjectPackage  
```  
  
 Cet attribut définit également le chemin d’accès de modèles pour pointer vers le dossier des modèles. Pour plus d’informations sur l’emplacement du dossier Modèles, consultez [prise en charge des modèles du Site Web](../../extensibility/internals/web-site-support-templates.md).  
  
## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute  
 Cet attribut est placé sur le projet de langage. Il permet au projet de Site Web d’imbriquer un type de fichier (lié) sous un autre type de fichier (principal) dans le **l’Explorateur de solutions**.  
  
 Exemple :  
  
```  
[WebSiteProjectRelatedFiles("aspx", "py")]public class PythonProjectPackage : ProjectPackage  
```  
  
 Spécifie qu’un fichier de code-behind IronPython est lié à un fichier .aspx. Lorsqu’une page Web .aspx est créée dans une solution de site Web de IronPython, un fichier source .py est généré et apparaît comme un nœud enfant de la page .aspx.  
  
## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute  
 Cet attribut est placé sur le package de projet de langage. Il sélectionne le fournisseur d’Intellisense pour la langue.  
  
 Exemple :  
  
```  
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]public class PythonPackage : Package, IOleComponent  
```  
  
 Spécifie qu’une instance de PythonIntellisenseProvider, qui implémente <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>, doit être créé à la demande pour fournir des services de langage.</xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>  
  
 L’implémentation de IVsIntellisenseProject traite les références et appelle le compilateur de langage lorsqu’une page Web avec le code est demandée mais n’est pas mis en cache.  
  
## <a name="see-also"></a>Voir aussi  
 [Prise en charge du Site Web](../../extensibility/internals/web-site-support.md)