---
title: ": Ca1820 Impossible de chaînes vides à l’aide de la longueur de chaîne | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
helpviewer_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
caps.latest.revision: "21"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7bfacf70dd1d23d0596815ad2f9fa3f51986aaad
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820 : Vérifiez la présence de chaînes vides par la longueur de chaîne
|||  
|-|-|  
|TypeName|TestForEmptyStringsUsingStringLength|  
|CheckId|CA1820|  
|Catégorie|Microsoft.Performance|  
|Modification avec rupture|Sans rupture|  
  
## <a name="cause"></a>Cause  
 Une chaîne est comparée à la chaîne vide à l’aide de <xref:System.Object.Equals%2A?displayProperty=fullName>.  
  
## <a name="rule-description"></a>Description de la règle  
 Comparer des chaînes à l’aide de la <xref:System.String.Length%2A?displayProperty=fullName> propriété ou le <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> méthode est nettement plus rapide que l’utilisation de <xref:System.Object.Equals%2A>. C’est parce que <xref:System.Object.Equals%2A> exécute des instructions MSIL beaucoup plus que <xref:System.String.IsNullOrEmpty%2A> ou le nombre d’instructions exécutées pour récupérer le <xref:System.String.Length%2A> propriété valeur et la comparer à zéro.  
  
 Vous devez être conscient que <xref:System.Object.Equals%2A> et <xref:System.String.Length%2A> == 0 se comportent différemment pour les chaînes null. Si vous essayez d’obtenir la valeur de la <xref:System.String.Length%2A> propriété sur une chaîne null, le common language runtime lève une <xref:System.NullReferenceException?displayProperty=fullName>. Si vous effectuez une comparaison entre une chaîne null et une chaîne vide, le common language runtime ne lève pas d’exception ; la comparaison retourne `false`. Test de la valeur null n’affecte pas considérablement les performances relatives de ces deux approches. Lorsque vous ciblez [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)], utilisez le <xref:System.String.IsNullOrEmpty%2A> (méthode). Sinon, utilisez le <xref:System.String.Length%2A> == comparaison chaque fois que possible.  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle, modifiez la comparaison à utiliser le <xref:System.String.Length%2A> propriété et test pour la chaîne de valeur null. Si le ciblage [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)], utilisez le <xref:System.String.IsNullOrEmpty%2A> (méthode).  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Il est possible de supprimer un avertissement de cette règle si les performances ne sont pas un problème.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant illustre les différentes techniques utilisées pour rechercher une chaîne vide.  
  
 [!code-csharp[FxCop.Performance.StringTest#1](../code-quality/codesnippet/CSharp/ca1820-test-for-empty-strings-using-string-length_1.cs)]