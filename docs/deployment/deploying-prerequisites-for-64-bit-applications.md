---
title: "Déploiement des composants requis pour les Applications 64 bits | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], 64-bit
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- 64-bit applications [Visual Studio]
ms.assetid: 87399e20-5510-41e4-b5b7-4a87c5773f21
caps.latest.revision: "23"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.openlocfilehash: aefb619487fba984e8f625dfe414c2f514f28c70
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="deploying-prerequisites-for-64-bit-applications"></a>Composants requis pour le déploiement d'applications 64 bits
Le déploiement ClickOnce prend en charge l'installation des applications sur les plateformes 64 bits. Les plateformes cibles sont **x86** pour les plateformes 32 bits, **x64** pour ordinateurs prenant en charge les jeux d’instructions AMD64 et EM64T, et **Itanium** pour le processeur Itanium 64 bits.  
  
## <a name="prerequisites"></a>Conditions préalables  
 Le tableau suivant répertorie les composants redistribuables que vous pouvez utiliser comme composants requis pour l'installation de votre application 64 bits.  
  
 Si vous sélectionnez un composant requis qui n'a pas de composants 64 bits, vous risquez de voir s'afficher un avertissement indiquant que les packages sélectionnés ne sont pas disponibles pour la plateforme 64 bits.  
  
|Composant redistribuable|Prise en charge x64|Prise en charge IA64|  
|---------------------|-----------------|------------------|  
|[!INCLUDE[vsto_runtime](../deployment/includes/vsto_runtime_md.md)]|Oui|Non|  
|Bibliothèques Runtime Visual C++ 2010 (IA64)|Non|Oui|  
|Bibliothèques Runtime Visual C++ 2010 (x64)|Oui|Non|  
|Microsoft .NET Framework 4 (x86 et x64)|Oui||  
|Microsoft .NET Framework 4 Client Profile (x86 et x64)|Oui||  
  
## <a name="see-also"></a>Voir aussi  
 [Déploiement d’Applications, Services et composants](../deployment/deploying-applications-services-and-components.md)   
 [Comment : installer les composants requis avec une Application ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Applications 64 bits](http://msdn.microsoft.com/Library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)