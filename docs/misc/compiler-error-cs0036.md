---
title: "Erreur du compilateur CS0036 | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0036"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0036"
ms.assetid: ddbaa36e-473b-4283-a13c-44a71ae5da2e
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Erreur du compilateur CS0036
Un paramètre out ne peut pas avoir l’attribut '\[In\]'  
  
 Actuellement, l’attribut **In** n’est pas autorisé pour un paramètre [out](/dotnet/csharp/language-reference/keywords/out).  
  
 L’exemple suivant génère l’erreur CS0036 :  
  
```  
// CS0036.cs using System; using System.Runtime.InteropServices; public class MyClass { public static void TestOut([In] out char TestChar)   // CS0036 // try the following line instead // public static void TestOut(out char TestChar) { TestChar = 'b'; Console.WriteLine(TestChar); } public static void Main() { char i;           //variable to receive the value TestOut(out i);   // the arg must be passed as out Console.WriteLine(i); } }  
```