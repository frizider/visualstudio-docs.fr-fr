---
title: Bytes_per_element, constante (Float64Array) | Documents Microsoft
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: e1afc629-4df3-49ce-baf5-5b51a6340621
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 84426b7b8e6920adb9a14b12696c6014b63ba997
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="bytesperelement-constant-float64array"></a>BYTES_PER_ELEMENT, constante (Float64Array)
Taille en octets de chaque élément contenu dans le tableau.  
  
## <a name="syntax"></a>Syntaxe  
  
```JavaScript  
var arraySize = int8Array.BYTES_PER_ELEMENT;  
```  
  
## <a name="example"></a>Exemple  
 L'exemple suivant montre comment obtenir la taille des éléments de tableau.  
  
```JavaScript  
var req = new XMLHttpRequest();  
    req.open('GET', "http://www.example.com");  
    req.responseType = "arraybuffer";  
    req.send();  
  
    req.onreadystatechange = function () {  
        if (req.readyState === 4) {  
            var buffer = req.response;  
            var dataView = new DataView(buffer);  
            var floatArr = new Float64Array(buffer.byteLength / 8);  
            alert(floatArr.BYTES_PER_ELEMENT);  
        }  
    }  
  
```  
  
## <a name="requirements"></a>Spécifications  
 [!INCLUDE[jsv10](../../javascript/reference/includes/jsv10-md.md)]