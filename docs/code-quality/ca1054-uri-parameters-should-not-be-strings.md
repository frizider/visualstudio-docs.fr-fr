---
title: "CA1054 : Les paramètres URI ne doivent pas être des chaînes | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA1054
- UriParametersShouldNotBeStrings
helpviewer_keywords:
- CA1054
- UriParametersShouldNotBeStrings
ms.assetid: 8e99d72b-a658-47a7-8dd5-9784ce2c30b8
caps.latest.revision: "14"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f965c200e7c020a151a0ffa8dc67f3b75e330bab
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054 : Les paramètres Uri ne doivent pas être des chaînes
|||  
|-|-|  
|TypeName|UriParametersShouldNotBeStrings|  
|CheckId|CA1054|  
|Catégorie|Microsoft.Design|  
|Modification avec rupture|Rupture|  
  
## <a name="cause"></a>Cause  
 Un type déclare une méthode avec un paramètre de chaîne dont le nom contient « uri », « Uri », « urn », « Urn », « url » ou « Url » et le type ne déclare pas une surcharge correspondante qui accepte un <xref:System.Uri?displayProperty=fullName> paramètre.  
  
## <a name="rule-description"></a>Description de la règle  
 Cette règle fractionne le nom de paramètre en jetons basés sur la convention de casse mixte et vérifie si chaque jeton est égal à « uri », « Uri », « urn », « Urn », « url » ou « Url ». Il existe une correspondance, la règle considère que le paramètre représente un identificateur de ressource uniforme (URI). Une représentation sous forme de chaîne d'un URI est sujette aux erreurs d'analyse et d'encodage, et peut entraîner des failles de sécurité. Si une méthode accepte une représentation sous forme de chaîne d’un URI, une surcharge correspondante doit être fournie qui prend une instance de la <xref:System.Uri> classe, qui fournit ces services de manière sûre et sécurisée.  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle, modifiez le paramètre pour un <xref:System.Uri> de type ; il s’agit d’une modification avec rupture. Vous pouvez également fournir une surcharge de la méthode qui prend un <xref:System.Uri> paramètre ; il s’agit d’une modification sans rupture.  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Il est possible de supprimer un avertissement de cette règle si le paramètre ne représente pas un URI.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant présente un type, `ErrorProne`, qui enfreint cette règle et un type, `SaferWay`, qui satisfait à la règle.  
  
 [!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1054-uri-parameters-should-not-be-strings_1.cs)]
 [!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1054-uri-parameters-should-not-be-strings_1.vb)]
 [!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1054-uri-parameters-should-not-be-strings_1.cpp)]  
  
## <a name="related-rules"></a>Règles associées  
 [CA1056 : Les propriétés d’URI ne doivent pas être des chaînes](../code-quality/ca1056-uri-properties-should-not-be-strings.md)  
  
 [CA1055 : Les valeurs de retour d’URI ne doivent pas être des chaînes](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)  
  
 [CA2234 : Passez des objets System.Uri au lieu de chaînes](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)  
  
 [CA1057 : Les surcharges d’URI de chaîne appellent des surcharges de System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)