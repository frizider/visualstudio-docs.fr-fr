---
title: "Guide pratique pour spécifier les emplacements du fichier de symboles à partir de la ligne de commande | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8aa067bb-e8bf-4081-aff0-cfbcf65934a0
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 63aad78bdc7df685ca3a73ec16a9cbc87b78151f
ms.openlocfilehash: 237acc5cc58646bc9f4e1ab6d2fbe976bb7ac124
ms.contentlocale: fr-fr
ms.lasthandoff: 07/14/2017

---
# Guide pratique pour spécifier les emplacements du fichier de symboles à partir de la ligne de commande
<a id="how-to-specify-symbol-file-locations-from-the-command-line" class="xliff"></a>
Pour afficher des informations de symboles telles que les noms de fonctions et les numéros de ligne, l’outil en ligne de commande VSPerfReport doit pouvoir accéder aux fichiers de symboles (.pdb) des composants profilés, ainsi qu’aux fichiers système Windows. Les fichiers de symboles sont créés lors de la compilation d’un composant. Pour plus d’informations, consultez [VSPerfReport](../profiling/vsperfreport.md). VSPerfReport recherche automatiquement les fichiers de symboles dans les emplacements suivants :  
  
-   Chemins spécifiés dans l’option **/SymbolPath** ou dans la variable d’environnement **_NT_SYMBOL_PATH**.  
  
-   Chemin local exact dans lequel un composant a été compilé.  
  
-   Répertoire contenant les données de profilage (.vsp ou .vsps).  
  
 Microsoft fournit les fichiers .pdb d’un grand nombre de ses produits en ligne sur un serveur de symboles. Si l’ordinateur que vous utilisez pour la génération de rapports est connecté à Internet, VSPerfReport se connecte au serveur de symboles en ligne afin de rechercher automatiquement les informations de symboles et d’enregistrer les fichiers dans un magasin local.  
  
 Vous pouvez spécifier l’emplacement des fichiers de symboles et de la banque de serveurs de symboles Microsoft en procédant de l’une des manières suivantes :  
  
-   Définissez la variable d’environnement **_NT_SYMBOL_PATH**.  
  
-   Ajoutez l’option **/SymbolPath** à la ligne de commande de VSPerfReport.  
  
 Vous pouvez également combiner ces deux méthodes.  
  
> [!NOTE]
>  Si [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] est installé sur l’ordinateur local, un emplacement pour les fichiers de symboles Windows a probablement déjà été défini. Pour plus d’informations, consultez [Guide pratique pour référencer les informations de symboles Windows](../profiling/how-to-reference-windows-symbol-information.md). Vous devez toujours configurer VSPerfReport pour utiliser l’emplacement et le serveur comme décrit plus loin dans cette rubrique.  
  
## Spécification des fichiers de symboles Windows
<a id="specifying-windows-symbol-files" class="xliff"></a>  
  
#### Pour configurer l’utilisation du serveur de symboles Windows
<a id="to-configure-the-use-of-the-windows-symbol-server" class="xliff"></a>  
  
1.  Si nécessaire, créez un répertoire dans lequel stocker les fichiers de symboles localement.  
  
2.  Utilisez la syntaxe suivante pour définir la variable d’environnement **_NT_SYMBOL_PATH** ou l’option VSPerfReport /SymbolPath :  
  
     **srv\*** *LocalStore* **\*http://msdl.microsoft.com/downloads/symbols**  
  
     où *LocalStore* est le chemin du répertoire local que vous avez créé.  
  
## Spécification des fichiers de symboles de composants
<a id="specifying-component-symbol-files" class="xliff"></a>  
 Les outils de profilage recherchent les fichiers .pdb des composants que vous voulez profiler dans leurs emplacements d’origine qui sont stockés dans les composants ou dans le dossier contenant le fichier des données de profilage. Vous pouvez spécifier d’autres emplacements dans lesquels effectuer la recherche en ajoutant un ou plusieurs chemins à **_NT_SYMBOL_PATH** ou à l’option **/SymbolPath**. Séparez les chemins par des points-virgules.  
  
## Exemple
<a id="example" class="xliff"></a>  
 La ligne de commande suivante définit le serveur de symboles Windows comme valeur de la variable d’environnement **_NT_SYMBOL_PATH** et **C:\Symbols** comme répertoire local.  
  
 **set  _NT_SYMBOL_PATH=srv\*C:\symbols\*http://msdl.microsoft.com/downloads/symbols**  
  
 La ligne de commande VSPerfReport suivante ajoute le répertoire C:\Projects\Symbols au chemin de recherche à l’aide de l’option **/SymbolPath**.  
  
 **VSPerfReport**  *MyApp* **.exe /SymbolPath:C:\Projects\Symbols /summary:all**