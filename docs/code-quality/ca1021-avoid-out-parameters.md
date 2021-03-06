---
title: "CA1021 : Éviter les paramètres out | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA1021
- AvoidOutParameters
helpviewer_keywords:
- AvoidOutParameters
- CA1021
ms.assetid: 970f2304-842c-4fb7-9734-f3871da8d479
caps.latest.revision: "19"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: dbefcb83efbcea76fec889b520f0cd0dd181bf9e
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca1021-avoid-out-parameters"></a>CA1021 : Éviter les paramètres out
|||  
|-|-|  
|TypeName|AvoidOutParameters|  
|CheckId|CA1021|  
|Catégorie|Microsoft.Design|  
|Modification avec rupture|Rupture|  
  
## <a name="cause"></a>Cause  
 Une méthode publique ou protégée dans un type public a un `out` paramètre.  
  
## <a name="rule-description"></a>Description de la règle  
 Passer des types par référence (à l’aide de `out` ou `ref`) nécessite une certaine expérience des pointeurs, de comprendre la différence entre les types valeur et les types référence et la gestion de méthodes impliquant plusieurs valeurs de retour. En outre, la différence entre `out` et `ref` paramètres est généralement peu comprise.  
  
 Lorsqu’un type référence est passé de « par référence », la méthode prévoit d’utiliser le paramètre pour retourner une instance différente de l’objet. Passez un type référence par référence est également appelé à l’aide du pointeur, pointeur vers un pointeur, ou une double indirection double. À l’aide de la valeur par défaut de convention d’appel, qui est de passer « par valeur », un paramètre qui accepte un type référence déjà reçoit un pointeur vers l’objet. Le pointeur, pas l’objet sur lequel il pointe, est passé par valeur. Passer par valeur signifie que la méthode ne peut pas modifier le pointeur afin qu’il pointe vers une nouvelle instance du type référence. Toutefois, il peut modifier le contenu de l’objet sur lequel il pointe. La plupart des applications, cela est suffisant et génère le comportement souhaité.  
  
 Si une méthode doit retourner une instance différente, utilisez la valeur de retour de la méthode pour y parvenir. Consultez la <xref:System.String?displayProperty=fullName> classe pour diverses méthodes qui opèrent sur des chaînes et retourner une nouvelle instance d’une chaîne. Lorsque ce modèle est utilisé, l’appelant doit décider si l’objet d’origine est conservé.  
  
 Bien que les valeurs de retour sont courants et très utilisées, l’application correcte de `out` et `ref` paramètres requiert de conception intermédiaire et de compétences en matière de codage. Architectes de bibliothèque de conception destiné à une audience générale ne doit pas s’attendre aux utilisateurs maîtrisent l’utilisation des `out` ou `ref` paramètres.  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle est dû à un type valeur, ont la méthode retourne l’objet comme sa valeur de retour. Si la méthode doit retourner plusieurs valeurs, reconcevoir pour retourner une seule instance d’un objet qui conserve les valeurs.  
  
 Pour corriger une violation de cette règle est dû à un type référence, assurez-vous que le comportement souhaité doit retourner une nouvelle instance de la référence. S’il s’agit, la méthode doit utiliser sa valeur de retour pour ce faire.  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Il est possible de supprimer un avertissement de cette règle. Toutefois, cette conception peut entraîner des problèmes d’utilisation.  
  
## <a name="example"></a>Exemple  
 La bibliothèque suivante présente deux implémentations d’une classe qui génère des réponses aux commentaires d’un utilisateur. La première implémentation (`BadRefAndOut`) force l’utilisateur de la bibliothèque à gérer trois valeurs de retour. La seconde implémentation (`RedesignedRefAndOut`) simplifie l’expérience utilisateur en retournant une instance d’une classe de conteneur (`ReplyData`) qui gère les données comme une unité unique.  
  
 [!code-csharp[FxCop.Design.NoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_1.cs)]  
  
## <a name="example"></a>Exemple  
 L’application suivante illustre l’expérience de l’utilisateur. L’appel à la nouvelle bibliothèque (`UseTheSimplifiedClass` méthode) est plus simple, et les informations retournées par la méthode sont facile à gérer. La sortie des deux méthodes est identique.  
  
 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_2.cs)]  
  
## <a name="example"></a>Exemple  
 La bibliothèque de l’exemple suivant illustre comment `ref` paramètres pour les types référence sont utilisés et affiche un meilleur moyen d’implémenter cette fonctionnalité.  
  
 [!code-csharp[FxCop.Design.RefByRefNo#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_3.cs)]  
  
## <a name="example"></a>Exemple  
 L’application suivante appelle chaque méthode dans la bibliothèque pour illustrer le comportement.  
  
 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_4.cs)]  
  
 Cet exemple produit la sortie suivante.  
  
 **Modification du pointeur - passé par valeur :**  
**12345**  
**12345**  
**Modification du pointeur - passé par référence :**  
**12345**  
**ABCDE 12345**  
**Le passage par valeur de retour :**  
**ABCDE 12345**   
## <a name="try-pattern-methods"></a>Essayez les méthodes de modèle  
  
### <a name="description"></a>Description  
 Les méthodes qui implémentent le **essayez\<quelque chose >** de modèle, par exemple <xref:System.Int32.TryParse%2A?displayProperty=fullName>, ne déclenchent pas cette violation. L’exemple suivant montre une structure (type valeur) qui implémente le <xref:System.Int32.TryParse%2A?displayProperty=fullName> (méthode).  
  
### <a name="code"></a>Code  
 [!code-csharp[FxCop.Design.TryPattern#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_5.cs)]  
  
## <a name="related-rules"></a>Règles associées  
 [CA1045 : Ne pas passer de types par référence](../code-quality/ca1045-do-not-pass-types-by-reference.md)