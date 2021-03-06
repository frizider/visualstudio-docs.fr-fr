---
title: "Avertissement de conformit&#233; CLS CLS01101 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CLS01101"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "CLS01101"
ms.assetid: 01034537-eee8-40e6-9139-d1788612738a
caps.latest.revision: 9
caps.handback.revision: 9
author: "corob-msft"
ms.author: "corob"
manager: "douge"
---
# Avertissement de conformit&#233; CLS CLS01101
Tous les types apparaissant dans une signature doivent être conformes CLS  
  
 Si un type est conforme CLS, tous les constructeurs présents dans ce type, sauf s’ils sont marqués comme étant non conformes CLS, doivent avoir des paramètres de type conformes CLS.  
  
 Pour plus d’informations sur la vérification de conformité CLS, consultez les [assemblys conformes CLS](http://msdn.microsoft.com/fr-fr/3320b57e-ea55-4697-a17d-f509a36a3c93).  
  
## Exemple  
 L’exemple suivant génère l’avertissement CLS01101 :  
  
```  
// CLS01101.cpp // compile with: /clr /LD // CLS01101 expected using namespace System; using namespace System::Reflection; [assembly:CLSCompliant (true)]; [assembly:AssemblyKeyFile("clscompliance.snk")]; [CLSCompliant(true)] public ref class CompliantType {}; [CLSCompliant(false)] public ref class NotCompliantType {}; [CLSCompliant(true)] public ref class One { public: One(NotCompliantType^ parameter) {}   // CLS01101 One(CompliantType^ parameter) {}   // OK [CLSCompliant(false)] One(NotCompliantType^ param1, NotCompliantType^ param2) {}   // OK };  
```