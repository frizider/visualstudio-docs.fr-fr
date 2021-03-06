---
title: "&lt;assemblyIdentity&gt; élément (déploiement ClickOnce) | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords: <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
caps.latest.revision: "20"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.openlocfilehash: db313077fa7903b2bdb2fbbe6b76aa80c940fecd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity&gt; élément (déploiement ClickOnce)
Identifie l’application déployée dans un [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] déploiement.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
      <assemblyIdentity   
   name  
   version  
   publicKeyToken  
   processorArchitecture  
   language  
/>  
```  
  
## <a name="elements-and-attributes"></a>Éléments et attributs  
 Le `assemblyIdentity` élément est requis. Il ne contienne aucun élément enfant et possède les attributs suivants.  
  
|Attribut|Description|  
|---------------|-----------------|  
|`Name`|Obligatoire. Identifie le nom de l’application.<br /><br /> Si `Name` contient des caractères spéciaux, tels que des guillemets simples ou doubles, l’application peut échouer à activer.|  
|`Version`|Obligatoire. Spécifie le numéro de version de l’application dans le format suivant :`major.minor.build.revision`|  
|`publicKeyToken`|Facultatif. Spécifie une chaîne hexadécimale de 16 caractères qui représente les 8 derniers octets de la `SHA-1` la valeur de la clé publique sous laquelle l’application ou l’assembly est signé de hachage. La clé publique qui est utilisée pour signer le catalogue doit être de 2 048 bits ou supérieur.<br /><br /> Bien que la signature d’un assembly est recommandée mais facultatif, cet attribut est obligatoire. Si un assembly n’est pas signé, vous devez copier une valeur à partir d’un assembly auto-signé ou utiliser une valeur « factice » de tous les zéros.|  
|`processorArchitecture`|Obligatoire. Spécifie le processeur. Les valeurs valides sont `msil` pour tous les processeurs, `x86` pour Windows 32 bits, `IA64` pour Windows 64 bits, et `Itanium` pour les processeurs Intel 64 bits Itanium.|  
|`language`|Obligatoire. Identifie les codes de langue de deux parties (par exemple, `en-US`) de l’assembly. Cet élément est dans le `asmv2` espace de noms. Si non spécifié, la valeur par défaut est `neutral`.|  
  
## <a name="examples"></a>Exemples  
  
### <a name="description"></a>Description  
 L’exemple de code suivant illustre un `assemblyIdentity` élément dans un [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifeste d’application. Cet exemple de code fait partie d’un exemple plus complet fourni dans [manifeste d’Application ClickOnce](../deployment/clickonce-application-manifest.md).  
  
### <a name="code"></a>Code  
  
```  
<asmv1:assemblyIdentity   
  name="My Application Deployment.exe"   
  version="1.0.0.0"   
  publicKeyToken="43cb1e8e7a352766"   
  language="neutral"   
  processorArchitecture="x86"   
  type="win32" />  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Manifeste d’Application ClickOnce](../deployment/clickonce-application-manifest.md)   
 [\<assemblyIdentity > élément](../deployment/assemblyidentity-element-clickonce-deployment.md)