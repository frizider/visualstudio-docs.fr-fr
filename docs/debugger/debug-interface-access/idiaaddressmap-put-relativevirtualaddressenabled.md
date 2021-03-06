---
title: IDiaAddressMap::put_relativeVirtualAddressEnabled | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d248c573ee9952fd3783f6994f5e0022c94ba436
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="idiaaddressmapputrelativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
Permet au client activer ou désactiver le calcul et l’utilisation des adresses virtuelles relatives (RVA).  
  
## <a name="syntax"></a>Syntaxe  
  
```C++  
HRESULT put_relativeVirtualAddressEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 NewVal  
 [in] La valeur `TRUE` pour activer, ou `FALSE` à désactiver.  
  
## <a name="return-value"></a>Valeur de retour  
 En cas de réussite, retourne `S_OK`; sinon, retourne un code d’erreur.  
  
## <a name="remarks"></a>Remarques  
 Pour les objets de débogage décrites par les interfaces DIA et par rapport à l’image de l’exécutable base, les adresses peuvent être récupérées en tant qu’adresses virtuelles relatives.  
  
 L’utilisation de RVA est activée lorsque les segments sont initialement chargées à partir d’un fichier PDB. Pour obtenir l’état actuel de l’utilisation de RVA, appelez le [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) (méthode).  
  
 Le `put_relativeVirtualAddress` méthode doit être appelée pour activer les RVA après un appel réussi pour le [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) méthode a établi les nouveaux en-têtes de l’image.  
  
## <a name="see-also"></a>Voir aussi  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)