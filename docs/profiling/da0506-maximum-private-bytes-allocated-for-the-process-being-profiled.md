---
title: "DA0506 : Octets privés alloués maximum au processus en cours de profilage | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.performance.rules.DA0506
- vs.performance.DA0506
- vs.performance.506
ms.assetid: e9c43554-9a85-4d98-9fa4-3b19986e7b62
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1a257478cf797741aee7f52361c59cbe06b72bc4
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="da0506-maximum-private-bytes-allocated-for-the-process-being-profiled"></a>DA0506 : Octets privés alloués maximum au processus en cours de profilage
|||  
|-|-|  
|ID de règle|DA0506|  
|Catégorie|Analyse des ressources|  
|Méthode de profilage|Tout|  
|Message|Uniquement à titre d’informations. Le compteur Octets privés de processus mesure la mémoire virtuelle allouée par le processus que vous profilez. La valeur signalée correspond à la valeur maximale observée dans l’ensemble des intervalles de mesure.|  
|Type de règle|Information|  
  
 Lorsque vous effectuez un profilage à l’aide de la méthode d’échantillonnage, de mémoire .NET ou de conflit des ressources, vous devez collecter au moins 10 échantillons pour déclencher cette règle.  
  
## <a name="rule-description"></a>Description de la règle  
 Ce message signale la quantité maximale de mémoire virtuelle actuellement allouée par le processus, en octets (octets privés). Les octets privés représentent les emplacements de mémoire virtuelle alloués par le processus et qui ne sont accessibles qu’aux threads actuellement exécutés dans le processus.  
  
 Pour un processus 32 bits s’exécutant sur un ordinateur 32 bits, la taille maximale de la partie privée de l’espace d’adressage de processus est de 2 Go. Avec le commutateur Boot.ini [/3GB](http://go.microsoft.com/fwlink/?LinkId=177831), les processus 32 bits peuvent acquérir jusqu’à 3 Go de mémoire virtuelle. Un processus 32 bits exécuté sur un ordinateur 64 bits peut acquérir jusqu’à 4 Go de mémoire virtuelle privée.  
  
 Un processus 64 bits exécuté sur un ordinateur 64 bits peut acquérir jusqu’à 8 To de mémoire virtuelle privée.  
  
 La valeur signalée correspond à la valeur maximale de tous les intervalles de mesure pendant lesquels le processus profilé était actif.  
  
 Pour plus d’informations sur les espaces d’adressage de processus, consultez [Espace d’adressage virtuel](http://go.microsoft.com/fwlink/?LinkId=177832) dans la documentation relative à la gestion de la mémoire dans Windows.  
  
## <a name="how-to-use-rule-data"></a>Comment utiliser des données de règle  
 Utilisez la valeur signalée pour comparer les performances des différentes versions du programme ou pour comprendre les performances de l’application dans différents scénarios de profilage.  
  
 Lorsqu’une valeur maximale d’octets privés de processus approche de la taille maximale autorisée pour un espace d’adressage de processus, pour son architecture, des exceptions de mémoire insuffisante peuvent être levées. Pour plus d’informations, consultez [Investigating Memory Issues](http://go.microsoft.com/fwlink/?LinkID=177833) dans MSDN Magazine.