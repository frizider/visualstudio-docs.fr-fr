---
title: "CA1726 : Utilisez les termes | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- UsePreferredTerms
- CA1726
helpviewer_keywords: UsePreferredTerms
ms.assetid: 642b2acd-3a33-4d1f-b0a7-67073ae73be2
caps.latest.revision: "23"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 2ae02d0eb136d45bc2b8af7dde5f897765493050
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ca1726-use-preferred-terms"></a>CA1726 : Utilisez les termes par défaut
|||  
|-|-|  
|TypeName|UsePreferredTerms|  
|CheckId|CA1726|  
|Catégorie|Microsoft.Naming|  
|Modification avec rupture|Avec rupture - lorsque déclenchée sur les assemblys<br /><br /> Sans rupture - lorsque déclenchée sur les paramètres de type|  
  
## <a name="cause"></a>Cause  
 Le nom d'un identificateur visible de l'extérieur contient un terme pour lequel un autre terme par défaut existe. Vous pouvez également le nom comprend le terme indicateur ou indicateurs.  
  
## <a name="rule-description"></a>Description de la règle  
 Cette règle analyse un identificateur dans des jetons. Chaque jeton unique et chaque combinaison de jetons doubles contigu sont comparée à des termes qui sont générés dans la règle et dans la section déconseillé des dictionnaires personnalisés. Le tableau suivant présente les termes qui sont intégrées à la règle et leurs solutions de remplacement par défaut.  
  
|Terme obsolète|Terme favori|  
|-------------------|--------------------|  
|ne sont pas|Ne sont pas|  
|Annulé|Canceled|  
|Impossible|Ne peut pas|  
|ComPlus|EnterpriseServices|  
|Couldnt|N’a pas pu|  
|N’a pas|DidNot|  
|Lecteur|Ne|  
|Ne pas|Ne pas|  
|Indicateur ou indicateurs|Il n’existe aucun terme de remplacement. Ne pas utiliser.|  
|n’était pas|HadNot|  
|N’a pas|HasNot|  
|ne l’avez pas|HaveNot|  
|Indices|Index|  
|n’est pas|IsNot|  
|Connexion|Ouverture de session|  
|Déconnexion|Fermeture de session|  
|Shouldnt|ShouldNot|  
|Authentification|Ouverture de session|  
|Approbation|Déconnexion|  
|Wasnt|WasNot|  
|n’ont pas été|N’ont pas été|  
|Impossible|WillNot|  
|Wouldnt|WouldNot|  
|Accessible en écriture|Accessible en écriture|  
  
## <a name="how-to-fix-violations"></a>Comment corriger les violations  
 Pour corriger une violation de cette règle, remplacez le terme par le terme de remplacement par défaut.  
  
## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements  
 Supprimer un avertissement de cette règle uniquement si le nom de l’identificateur se rapporte intentionnellement et spécifiquement au terme d’origine au lieu du terme favori.  
  
## <a name="related-rules"></a>Règles associées  
 [Avertissements liés à l’affectation de noms](../code-quality/naming-warnings.md)