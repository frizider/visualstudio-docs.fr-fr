---
title: CV_call_e | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
caps.latest.revision: "10"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 89340c4cd448201f7624f5ec6b15dc67f74db4f6
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="cvcalle"></a>CV_call_e
Spécifie la convention d’appel pour une fonction.  
  
> [!NOTE]
>  Seules les valeurs d’énumération courants décrits ici. L’énumération complète est disponible dans le fichier d’en-tête cvconst.h.  
  
## <a name="syntax"></a>Syntaxe  
  
```C++  
typedef enum CV_call_e {   
   CV_CALL_NEAR_C    = 0x00,  
   CV_CALL_NEAR_FAST = 0x04,  
   CV_CALL_NEAR_STD  = 0x07,  
   CV_CALL_NEAR_SYS  = 0x09,  
   CV_CALL_THISCALL  = 0x0b,  
   CV_CALL_CLRCALL   = 0x16  
} CV_call_e;  
```  
  
## <a name="elements"></a>Éléments  
 CV_CALL_NEAR_C  
 Spécifie une convention d’appel de fonction à l’aide d’un push proche de droite à gauche. La fonction appelante efface la pile.  
  
 CV_CALL_NEAR_FAST  
 Spécifie une convention d’appel de fonction à l’aide d’un push de gauche à droite near avec les registres. La fonction appelée utilise la somme des octets de paramètres pour effacer la pile.  
  
 CV_CALL_NEAR_STD  
 Spécifie une convention d’appel de fonction via un appel standard near (push de droite à gauche).  
  
 CV_CALL_NEAR_SYS  
 Spécifie une convention d’appel de fonction à l’aide d’un appel système proche.  
  
 CV_CALL_THISCALL  
 Spécifie une convention d’appel de fonction à l’aide `this` appeler (`this` pointeur passé dans le Registre).  
  
 CV_CALL_CLRCALL  
 Spécifie une convention d’appel de fonction utilisée par le Common Language Runtime (CLR) (également appelé un code managé convention d’appel).  
  
## <a name="remarks"></a>Remarques  
 Les valeurs de cette énumération sont retournées par un appel à la [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) (méthode).  
  
## <a name="requirements"></a>Spécifications  
 En-tête : cvconst.h  
  
## <a name="see-also"></a>Voir aussi  
 [Énumérations et Structures](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)