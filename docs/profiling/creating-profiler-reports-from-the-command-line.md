---
title: "Création de rapports de profileur à partir de la ligne de commande | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c886f8af-2014-4fec-9b24-d98b68ecafb7
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5beb7a3db1e62937435ed7379c5f02e77c4f0795
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="creating-profiler-reports-from-the-command-line"></a>Création de rapports de profileur à partir de la ligne de commande
L’outil en ligne de commande **VSPerfReport** vous permet de créer des rapports .xml ou .csv (valeurs séparées par des virgules) à partir de fichiers de données de profilage (.vsp). Les types de rapport de VSPerfReport correspondent étroitement aux vues de type tableau de l’interface de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Vous pouvez filtrer le rapport pour voir seulement votre code et un segment du fichier de données de profilage. Pour plus d’informations, consultez [VSPerfReport](../profiling/vsperfreport.md).  
  
 Vous pouvez aussi rendre vos fichiers de données de profilage plus faciles à partager en incorporant des symboles dans les fichiers .vsp et en créant des fichiers de rapport pré-analysés (.vsps), qui sont plus petits et plus rapides à ouvrir.  
  
## <a name="common-tasks"></a>Tâches courantes  
  
|Tâche|Contenu associé|  
|----------|---------------------|  
|**Créer un rapport de base** Créez tout ou partie des types de rapports de VSPerfReport.|-   [Création de rapports de base](../profiling/creating-basic-profiling-reports-from-the-command-line.md)|  
|**Comparez deux fichiers de données de profilage.** Créez un rapport différentiel qui compare les données de performances dans deux fichiers de données de profilage.|-   [Guide pratique pour créer un rapport de comparaison du profileur à partir d’une invite de commandes](../profiling/how-to-create-a-profiler-comparison-report-from-a-command-prompt.md)|  
|**Afficher les données de suivi des appels et de suivi d’événements pour Windows (ETW)** Créez un rapport de suivi des appels qui répertorie les informations chronologiques de chaque point d’entrée et de sortie des fonctions de votre application, et de chaque appel effectué par votre fonction à d’autres fonctions. Vous pouvez aussi créer une liste détaillée de tous les événements du suivi d’événements pour Windows qui ont été collectés dans une exécution du profilage.|-   [Guide pratique pour créer un rapport de suivi d’appels](../profiling/how-to-create-a-profiling-tools-call-trace-report.md)|  
|**Filtrer un rapport.** Limitez un rapport aux seules fonctions de votre code ou à un moment spécifique dans le fichier de données de profilage.|-   [Guide pratique pour filtrer des rapports à partir de la ligne de commande](../profiling/how-to-filter-reports-from-the-command-line.md)|  
|**Créez des fichiers de données de profilage portables.** Pour rendre le partage des données de profilage plus facile, vous pouvez incorporer les symboles pour une exécution de profilage dans le fichier .vsp. Vous pouvez également créer un fichier de données de profilage pré-analysé (.vsps), qui est plus petit et plus rapide à ouvrir.|-   [Création de fichiers de données de profilage portables](../profiling/creating-portable-profiling-data-files-from-the-command-line.md)|