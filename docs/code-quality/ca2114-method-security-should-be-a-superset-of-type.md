---
title: "CA2114 : Sécurité de la méthode doit être un sur-ensemble du type | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- MethodSecurityShouldBeASupersetOfType
- CA2114
helpviewer_keywords:
- CA2114
- MethodSecurityShouldBeASupersetOfType
ms.assetid: 663f7aa4-8be5-4bd5-be92-4e9444f07077
caps.latest.revision: "17"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d9784ae650a411ef4fe5086ae8bf756147fd2365
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114 :La sécurité de la méthode doit être un sur-ensemble du type
|||  
|-|-|  
|TypeName|MethodSecurityShouldBeASupersetOfType|  
|CheckId|CA2114|  
|Catégorie|Microsoft.Security|  
|Modification avec rupture|Rupture|  
  
## <a name="cause"></a>Cause  
 Un type a la sécurité déclarative, une de ses méthodes présente une sécurité déclarative pour la même action de sécurité et l’action de sécurité n’est pas [les demandes de liaison](/dotnet/framework/misc/link-demands) ou [des demandes d’héritage](http://msdn.microsoft.com/en-us/28b9adbb-8f08-4f10-b856-dbf59eb932d9)et les autorisations vérifiées par le type ne sont pas un sous-ensemble des autorisations vérifiées par la méthode.  
  
## <a name="rule-description"></a>Description de la règle  
 Une méthode ne doit pas avoir à la fois une sécurité déclarative au niveau méthode et au niveau type pour la même action. Les deux contrôles ne sont pas combinés ; uniquement la demande de niveau de la méthode est appliquée. Par exemple, si un type demande une autorisation `X`, et une de ses méthodes demande une autorisation `Y`, code ne doit pas avoir l’autorisation `X` pour exécuter la méthode.  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Examinez votre code pour vous assurer que les deux actions sont requises. Si les deux actions sont requises, assurez-vous que l’action de niveau de la méthode inclut la sécurité spécifiée au niveau du type. Par exemple, si votre type demande une autorisation `X`, et sa méthode doit également demander une autorisation `Y`, la méthode doit demander explicitement `X` et `Y`.  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Il est possible de supprimer un avertissement de cette règle si la méthode ne requiert pas la sécurité spécifiée par le type. Toutefois, ce scénario n’est pas ordinaire et peut indiquer la nécessité d’un examen approfondi du design.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant utilise des autorisations d’environnement pour illustrer les risques de violation de cette règle. Dans cet exemple, le code d’application crée une instance du type sécurisé avant de refuser l’autorisation requise par le type. Dans un scénario de menace réel, l’application nécessite une autre méthode pour obtenir une instance de l’objet.  
  
 Dans l’exemple suivant, la bibliothèque demande autorisation d’écriture pour un type et une autorisation pour une méthode de lecture.  
  
 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../code-quality/codesnippet/CSharp/ca2114-method-security-should-be-a-superset-of-type_1.cs)]  
  
## <a name="example"></a>Exemple  
 Le code d’application suivant montre la vulnérabilité de la bibliothèque en appelant la méthode, même si elle ne répond pas aux exigences de sécurité de niveau type.  
  
 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../code-quality/codesnippet/CSharp/ca2114-method-security-should-be-a-superset-of-type_2.cs)]  
  
 Cet exemple produit la sortie suivante.  
  
 **[Toutes les autorisations] Les informations personnelles : 6/16/1964 12:00:00 AM**  
**[Aucune autorisation d’écriture (exigée par type)] Les informations personnelles : 6/16/1964 12:00:00 AM**  
**[Aucune autorisation de lecture (exigée par méthode)] Peut pas accéder aux données personnelles : échouée de la demande.**   
## <a name="see-also"></a>Voir aussi  
 [Instructions de codage sécurisé](/dotnet/standard/security/secure-coding-guidelines)   
 [Demandes d’héritage](http://msdn.microsoft.com/en-us/28b9adbb-8f08-4f10-b856-dbf59eb932d9)   
 [Demandes de liaison](/dotnet/framework/misc/link-demands)   
 [Données et modélisation](/dotnet/framework/data/index)