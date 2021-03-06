---
title: "CA2212 : Ne marquez pas les composants pris en charge avec WebMethod | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
helpviewer_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
ms.assetid: 774bc55d-e588-48ee-8f38-c228580feca2
caps.latest.revision: "13"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 44c29215301212a12c5652fbf1fe91af23db1082
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca2212-do-not-mark-serviced-components-with-webmethod"></a>CA2212 : Ne marquez pas les composants pris en charge avec WebMethod
|||  
|-|-|  
|TypeName|DoNotMarkServicedComponentsWithWebMethod|  
|CheckId|CA2212|  
|Catégorie|Microsoft.Usage|  
|Modification avec rupture|Rupture|  
  
## <a name="cause"></a>Cause  
 Une méthode dans un type qui hérite de <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> est marquée avec <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>.  
  
## <a name="rule-description"></a>Description de la règle  
 <xref:System.Web.Services.WebMethodAttribute>s’applique aux méthodes au sein d’un service Web XML qui ont été créés à l’aide d’ASP.NET ; Il rend la méthode peut être appelée à partir de clients Web distants. La méthode et la classe doivent être publique et en cours d’exécution dans une application Web ASP.NET. <xref:System.EnterpriseServices.ServicedComponent>types sont hébergés par les applications COM + et peuvent utiliser les services COM +. <xref:System.Web.Services.WebMethodAttribute>n’est pas appliquée à <xref:System.EnterpriseServices.ServicedComponent> types, car elles ne sont pas prévues pour les mêmes scénarios. En particulier, en ajoutant l’attribut à la <xref:System.EnterpriseServices.ServicedComponent> méthode ne rend pas la méthode peut être appelée à partir de clients Web distants. Étant donné que <xref:System.Web.Services.WebMethodAttribute> et un <xref:System.EnterpriseServices.ServicedComponent> méthode ont des comportements incompatibles et la configuration requise pour le contexte et de flux de transaction, le comportement de la méthode est incorrect dans certains scénarios.  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle, supprimez l’attribut de la <xref:System.EnterpriseServices.ServicedComponent> (méthode).  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Ne supprimez aucun avertissement de cette règle. Il n’existe pas de scénarios où la combinaison de ces éléments est correct.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName>   
 <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>