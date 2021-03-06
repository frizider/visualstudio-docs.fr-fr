---
title: Les pseudo-variables | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Watch window, pseudovariables
- debugging [Visual Studio], pseudovariables
- pseudovariables
ms.assetid: fae84f68-2138-4144-9bd4-c9e271b6182a
caps.latest.revision: "35"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b92b070641e4eed47b0094e1611f78cd799e6952
ms.sourcegitcommit: 26419ab0cccdc30d279c32d6a841758cfa903806
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2017
---
# <a name="pseudovariables-in-the-visual-studio-debugger"></a>Pseudo-variables dans le débogueur Visual Studio
Les pseudo-variables sont des termes utilisés pour afficher certaines informations dans une fenêtre de variable ou la **Espion express** boîte de dialogue. Vous pouvez entrer une pseudo-variable de la même façon qu'une variable normale. Toutefois, les pseudo-variables ne sont pas des variables et ne correspondent pas à des noms de variable de votre programme.  
  
## <a name="example"></a>Exemple  
 Supposez que vous écrivez une application en code natif et que vous voulez afficher le nombre de handles alloués à votre application. Dans le **espion** fenêtre, vous pouvez entrer la pseudo-variable suivante dans le **nom** colonne, puis appuyez sur ENTRÉE pour l’évaluer :  
  
```  
$handles  
```  
  
 En code natif, vous pouvez utiliser les pseudo-variables indiquées dans le tableau suivant :  
  
|Pseudo-variable|Fonction|  
|--------------------|--------------|  
|`$err`|Affiche la dernière valeur d'erreur définie avec la fonction SetLastError. La valeur affichée représente la valeur retournée par la fonction GetLastError.<br /><br /> Utilisez `$err,hr` pour afficher cette valeur sous une forme décodée. Par exemple, si la dernière erreur est 3, `$err,hr` affiche `ERROR_PATH_NOT_FOUND : The system cannot find the path specified.`|  
|`$handles`|Affiche le nombre de handles alloués à votre application.|  
|`$vframe`|Affiche l'adresse du frame de pile actuel.|  
|`$tid`|Affiche l'ID du thread actuel.|  
|`$env`|Affiche le bloc environnement de l'explorateur de chaînes.|  
|`$cmdline`|Affiche la chaîne de ligne de commande qui a lancé le programme.|  
|`$pid`|Affiche l'ID du processus.|  
|`$`*registername*<br /><br /> ou<br /><br /> `@`*registername*|Affiche le contenu du Registre *registername*.<br /><br /> En règle générale, vous pouvez afficher le contenu du registre en entrant simplement son nom. Vous n'avez besoin d'utiliser cette syntaxe que lorsque le nom de registre surcharge le nom d'une variable. Si le nom de registre est le même que celui d'une variable dans la portée actuelle, le débogueur interprète le nom comme étant celui de la variable. C'est-à-dire quand `$` *registername* ou `@` *registername* s’avère pratique.|  
|`$clk`|Affiche le temps en cycles d'horloge.|  
|`$user`|Affiche une structure avec les informations du compte qui exécute l'application. Pour des raisons de sécurité, les informations de mot de passe ne sont pas affichées.|  
|`$exceptionstack`|Affiche l'arborescence des appels de procédure de l'exception Windows Runtime actuelle. `$ exceptionstack`fonctionne uniquement dans les applications UWP et Windows 8.1 ou version ultérieure. `$ exceptionstack` n'est pas pris en charge pour les exceptions C++ et SHE|  
|`$ReturnValue`|Affiche la valeur de retour d'une méthode .NET Framework.|  
  
 En C# et Visual Basic, vous pouvez utiliser les pseudo-variables indiquées dans le tableau suivant :  
  
|Pseudo-variable|Fonction|  
|--------------------|--------------|  
|`$exception`|Affiche des informations sur la dernière exception. Si aucune exception ne s'est produite, l'évaluation de `$exception` affiche un message d'erreur.<br /><br /> En Visual c# uniquement, lorsque l’Assistant Exception est désactivé, `$exception` est automatiquement ajouté à la **variables locales** fenêtre lorsqu’une exception se produit.|  
|`$user`|Affiche une structure avec les informations du compte qui exécute l'application. Pour des raisons de sécurité, les informations de mot de passe ne sont pas affichées.|  
  
 En Visual Basic, vous pouvez utiliser les pseudo-variables indiquées dans le tableau suivant :  
  
|Pseudo-variable|Fonction|  
|--------------------|--------------|  
|`$delete` ou `$$delete`|Supprime une variable implicite créée dans le **exécution** fenêtre. La syntaxe est `$delete,` *variable* ou`$delete,` *variable*`.`|  
|`$objectids` ou `$listobjectids`|Affiche tous les ID d'objet actifs en tant qu'enfants de l'expression spécifiée. La syntaxe est `$objectid,` *expression* ou`$listobjectids,` *expression*`.`|  
|`$`*N*`#`|Affiche l’objet avec l’ID d’objet égal à *N*.|  
|`$dynamic`|Affiche le spécial **affichage dynamique** nœud pour un objet qui implémente le `IDynamicMetaObjectProvider`. Interface. La syntaxe est `$dynamic,` *objet*. Cette fonctionnalité s’applique uniquement au code utilisant .NET Framework version 4.|  
  
## <a name="see-also"></a>Voir aussi  
 [Espion et Espion express, fenêtres](../debugger/watch-and-quickwatch-windows.md)   
 [Fenêtres de variables](../debugger/debugger-windows.md)