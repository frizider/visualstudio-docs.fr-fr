---
title: "Comment : créer des extraits de code XML | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d8556dd7-1382-4af7-ba80-3e873c9416be
caps.latest.revision: "2"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 36fccee0e228e4391e80388284b59f19e1f3a1b9
ms.sourcegitcommit: c0422a3d594ea5ae8fc03f1aee684b04f417522e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2017
---
# <a name="how-to-create-xml-snippets"></a>Procédure : créer des extraits XML
Vous pouvez utiliser l'éditeur XML pour créer de nouveaux extraits XML. Cet éditeur comporte un extrait XML appelé « Snippet », qui est souvent utilisé pour la création de nouveaux extraits XML.  
  
## <a name="to-create-a-new-xml-snippet"></a>Pour créer un nouvel extrait XML  
 Pour créer un nouveau code XML extrait de créer un nouveau fichier XML et utilisez la **insérer un extrait** fonctionnalité.  
  
1.  Sur le **fichier** menu, cliquez sur **nouveau** puis cliquez sur **fichier**.  
  
2.  Cliquez sur **fichier XML** puis cliquez sur **ouvrir**.  
  
3.  Avec le bouton droit dans le volet de l’éditeur et sélectionnez **insérer un extrait**.  
  
4.  Sélectionnez **extrait** à partir de la liste et appuyez sur ENTRÉE.  
  
5.  Apportez les modifications voulues au nouvel extrait.  
  
6.  À partir de la **fichier** menu Sélectionnez **Enregistrer XMLFile.xml**.  
  
     Le **enregistrer le fichier sous** boîte de dialogue s’affiche.  
  
7.  Entrez le nom du nouvel extrait et sélectionnez **extrait les fichiers** à partir de la **enregistrer en tant que type** fenêtre déroulante.  
  
8.  Utilisez le **enregistrer dans** liste déroulante pour modifier l’emplacement du fichier au dossier par Mes Documents\Visual Studio 2005\Code Snippets\XML\My XML Snippets, puis appuyez sur **enregistrer**.  
  
## <a name="snippet-description"></a>Description des extraits  
 Cette section décrit certains éléments clés de l'extrait souvent utilisé. Pour plus d’informations sur les éléments de schéma utilisés par les extraits XML, consultez [référence du schéma des extraits de Code](../ide/code-snippets-schema-reference.md).  
  
### <a name="snippettype-element"></a>Élément SnippetType  
 L'éditeur prend en charge deux types d'extraits :  
  
```xml
<SnippetTypes>  
  <SnippetType>SurroundsWith</SnippetType>  
  <SnippetType>Expansion</SnippetType>  
</SnippetTypes>  
```  
  
 Le `Expansion` type détermine si l’extrait apparaît lorsque vous appelez le **insérer un extrait** commande. Le `SurroundsWith` type détermine si l’extrait apparaît lorsque vous appelez le **entourer** commande.  
  
### <a name="code-element"></a>Élément Code  
 L'élément `Code` définit le texte XML qui sera inséré lorsque l'extrait sera appelé.  
  
> [!NOTE]
>  Le texte de l'extrait XML doit être placé dans une section `<![CDATA[...]]>`.  
  
 L'élément `Code` suivant est créé par l'extrait souvent utilisé.  
  
```xml
<Code Language="XML">  
  <![CDATA[<test>  
  <name>$name$</name>  
  $selected$ $end$</test>]]>  
</Code>  
```  
  
 L'élément `Code` inclut trois variables.  
  
-   $name$ est une variable définie par l'utilisateur. Elle crée un élément `name` dont la valeur par défaut modifiable est « name ». Les variables définies par l'utilisateur se définissent à l'aide de l'élément `Literal`.  
  
-   $selected$ est une variable prédéfinie. Elle représente le texte sélectionné dans l'éditeur XML avant l'appel de l'extrait. La position de cette variable détermine l'emplacement du texte sélectionné dans l'extrait de code qui entoure cette sélection.  
  
-   $end$ est une variable prédéfinie. Lorsque l'utilisateur appuie sur ENTRÉE pour terminer l'édition des champs de l'extrait de code, cette variable détermine l'endroit où le signe ^ est placé.  
  
 L'élément `Code` ci-dessus insère le texte XML suivant :  
  
```xml
<test>  
  <name>name</name>  
</test>  
```  
  
 La valeur de l'élément name est marquée comme une zone modifiable.  
  
### <a name="literal-element"></a>Élément Literal  
 L'élément `Literal` permet d'identifier le texte de remplacement qui peut être personnalisé après son insertion dans le fichier. Par exemple, des chaînes littérales, des valeurs numériques et certains noms de variables peuvent être déclarés comme littéraux. Vous pouvez définir un nombre quelconque de littéraux dans votre extrait XML et y faire référence plusieurs fois dans l'extrait. L'exemple d'élément `Literal` suivant définit une variable $name$ dont la valeur par défaut est « name ».  
  
```xml
<Literal>  
  <ID>name</ID>  
  <Default>name</Default>  
</Literal  
```  
  
 Les littéraux peuvent également faire référence à des fonctions. L’éditeur XML comprend une fonction nommée **LookupPrefix**. Le **LookupPrefix** fonction recherche l’URI d’espace de noms donné à partir de l’emplacement dans le document XML de cet extrait est appelé et retourne le préfixe d’espace de noms qui est défini pour cet espace de noms, si un, et elle inclut les deux-points ( :)) Dans ce nom. Voici un exemple d’un `Literal` élément qui utilise le **LookupPrefix** (fonction).  
  
```xml
<Literal Editable="false">  
   <ID>prefix</ID>  
   <Function>LookupPrefix("namespaceURI")</Function>  
</Literal>  
```  
  
 La variable $prefix$ _peut alors être utilisée ailleurs dans votre extrait XML.  
  
## <a name="see-also"></a>Voir aussi  
 [Extraits XML](../xml-tools/xml-snippets.md)   
 [Comment : utiliser des extraits XML](../xml-tools/how-to-use-xml-snippets.md)   
 [Guide pratique pour générer un extrait XML à partir d’un schéma XML](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)