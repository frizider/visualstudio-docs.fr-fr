---
title: "Erreur du compilateur CS0104 | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0104"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0104"
ms.assetid: 1a7e9ae8-308b-441b-ba85-fac974222875
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Erreur du compilateur CS0104
'référence' est une référence ambiguë entre 'identificateur' et 'identificateur’  
  
 Votre programme contient des directives [using](/dotnet/csharp/language-reference/keywords/using) pour deux espaces de noms et votre code fait référence à un nom qui apparaît dans les deux espaces de noms.  
  
 L’exemple suivant génère l’erreur CS0104 :  
  
```  
// CS0104.cs using x; using y; namespace x { public class Test { } } namespace y { public class Test { } } public class a { public static void Main() { Test test = new Test();   // CS0104, is Test in x or y namespace? // try the following line instead // y.Test test = new y.Test(); } }  
```