---
title: "Op&#233;rateur de contexte (C++) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.operators"
dev_langs: 
  - "FSharp"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "expressions [C++], débogueur natif"
  - "évaluation"
  - "spécificateurs de format, expressions"
  - "opérateur de contexte, dans les expressions"
  - "débogage [C++], expressions"
  - "évaluateur d’expressions natives"
ms.assetid: 73cc9afe-f4a4-474e-bb89-5a33fb5e570c
caps.latest.revision: 23
caps.handback.revision: 23
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
---
# Op&#233;rateur de contexte (C++)
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

Vous pouvez utiliser l’opérateur de contexte en C\+\+ pour qualifier l’emplacement d’un point d’arrêt, un nom de variable ou une expression. L’opérateur de contexte est utile pour spécifier un nom issu d’une portée externe qui serait sinon masqué par un nom local.  
  
##  <a name="BKMK_Using_context_operators_to_specify_a_symbol"></a> Syntaxe  
 Il existe deux façons de spécifier le contexte :  
  
1.  {,,\[*module*\] } *expression*  
  
     Les accolades doivent contenir deux virgules et le nom ou le chemin complet du module \(fichier exécutable ou DLL\).  
  
     Par exemple, pour définir un point d’arrêt dans la fonction `SomeFunction` de EXAMPLE.dll :  
  
    ```cpp  
    {,,EXAMPLE.dll}SomeFunction  
    ```  
  
2.  *module*\!*expression*  
  
    ```cpp  
    EXAMPLE.dll!SomeFunction  
    ```  
  
-   *module* est le nom d’un module. Vous pouvez utiliser un chemin complet pour distinguer les modules portant le même nom.  
  
     Si le chemin du *module* comprend une virgule, un espace incorporé ou une accolade, vous devez utiliser des guillemets au début et à la fin du chemin afin que l’analyseur de contexte reconnaisse la chaîne. Les guillemets simples sont considérés comme faisant partie d’un nom de fichier Windows, c’est pourquoi vous devez utiliser des guillemets doubles. Par exemple :  
  
    ```  
    {,"a long, long, library name.dll", } g_Var  
    ```  
  
-   *expression* correspond à une expression C\+\+ valide qui correspond à une cible valide, telle qu’un nom de fonction, un nom de variable ou une adresse de pointeur dans *module*.  
  
 Lorsque l’évaluateur d’expression rencontre un symbole dans une expression, il recherche le symbole en procédant dans l’ordre suivant :  
  
1.  Portée lexicale, vers l’extérieur, du bloc actuel \(série d’instructions entre accolades\) au bloc englobant. Le bloc actuel est le code contenant l’emplacement actuel \(adresse du pointeur d’instruction\).  
  
2.  Portée de la fonction. La fonction actuelle.  
  
3.  Portée de la classe, si l’emplacement actuel se trouve à l’intérieur d’une fonction membre C\+\+. La portée de la classe comprend toutes les classes de base. L’évaluateur d’expression utilise les règles de dominance classiques.  
  
4.  Symboles globaux dans le module actuel.  
  
5.  Symboles publics dans le programme actuel.