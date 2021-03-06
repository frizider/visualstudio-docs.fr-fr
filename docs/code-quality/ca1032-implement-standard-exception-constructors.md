---
title: "CA1032 : Implémenter des constructeurs d’exception standard | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
caps.latest.revision: "16"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7300465ce9cef97cf322a7667e775852e22edb4e
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032 : Implémenter des constructeurs d'exception standard
|||  
|-|-|  
|TypeName|ImplementStandardExceptionConstructors|  
|CheckId|CA1032|  
|Catégorie|Microsoft.Design|  
|Modification avec rupture|Sans rupture|  
  
## <a name="cause"></a>Cause  
 Un type étend <xref:System.Exception?displayProperty=fullName> et ne déclare pas tous les constructeurs requis.  
  
## <a name="rule-description"></a>Description de la règle  
 Types d’exception doivent implémenter les constructeurs suivants :  
  
-   NewException() public  
  
-   NewException(string) public  
  
-   publique NewException (string, Exception)  
  
-   NewException protégée ou privée (SerializationInfo, StreamingContext)  
  
 Ne pas fournir le jeu complet de constructeurs peut rendre difficile une gestion des exceptions correcte. Par exemple, le constructeur qui possède la signature `NewException(string, Exception)` est utilisé pour créer des exceptions provoquées par d’autres exceptions. Sans ce constructeur Impossible de créer et de lever une instance de votre exception personnalisée qui contient l’exception interne (imbriquée), qui est le code managé doit effectuer dans une telle situation. Les premiers constructeurs de trois exception sont publics par convention. Le quatrième constructeur est protégé dans les classes non scellés et privé dans les classes sealed. Pour plus d’informations, consultez [CA2229 : implémentez des constructeurs de sérialisation](../code-quality/ca2229-implement-serialization-constructors.md)  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle, ajoutez les constructeurs manquants à l’exception et assurez-vous qu’ils disposent de l’accessibilité appropriée.  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Il est possible de supprimer un avertissement de cette règle quand la violation est due à l’aide d’un niveau d’accès différent pour les constructeurs publics.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant contient un type d’exception qui enfreint cette règle et un type d’exception qui est implémenté correctement.  
  
 [!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../code-quality/codesnippet/CSharp/ca1032-implement-standard-exception-constructors_1.cs)]