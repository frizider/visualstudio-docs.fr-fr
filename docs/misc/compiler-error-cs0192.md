---
title: "Erreur du compilateur CS0192 | Microsoft Docs"
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
  - "CS0192"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0192"
ms.assetid: d3fb6d18-dbf3-42c3-a280-afe55b97c2d1
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Erreur du compilateur CS0192
Impossible de passer les champs d’un champ readonly statique 'nom' en ref ou out \(sauf s’ils appartiennent à un constructeur statique\)  
  
 Un champ \(variable\) marqué avec le mot clé [readonly](/dotnet/csharp/language-reference/keywords/readonly) ne peut pas être passé à un paramètre [ref](/dotnet/csharp/language-reference/keywords/ref) ou [out](/dotnet/csharp/language-reference/keywords/out), sauf à l’intérieur d’un constructeur. Pour plus d'informations, consultez [Champs](/dotnet/csharp/programming-guide/classes-and-structs/fields).  
  
 L’erreur CS0192 se produit également si le champ `readonly` est [static](/dotnet/csharp/language-reference/keywords/static) et que le constructeur n’est pas marqué `static`.  
  
## Exemple  
 L’exemple suivant génère l’erreur CS0192 :  
  
```  
// CS0192.cs class MyClass { public readonly int TestInt = 6; static void TestMethod(ref int testInt) { testInt = 0; } MyClass() { TestMethod(ref TestInt);   // OK } public void PassReadOnlyRef() { TestMethod(ref TestInt);   // CS0192 } public static void Main() { } }  
```