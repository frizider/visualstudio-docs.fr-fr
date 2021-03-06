---
title: IEEDataStorage::GetData | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IEEDataStorage::GetData
helpviewer_keywords: IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
caps.latest.revision: "7"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ae4d4e371a79178be741e45662f4a8db8680b5ab
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
Récupère le nombre spécifié d’octets à partir de l’objet.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetData(  
   ULONG  dataSize,  
   ULONG* sizeGotten,  
   BYTE*  data  
);  
```  
  
```csharp  
int GetData(  
   uint     dataSize,  
   out uint sizeGotten,  
   byte[]   data  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `dataSize`  
 [in] Le nombre d’octets à récupérer (la `data` tableau doit contenir au moins ce nombre d’octets).  
  
 `sizeGotten`  
 [out] Retourne le nombre d’octets réellement récupérées.  
  
 `data`  
 [dans, out] Tableau à remplir avec les données demandées.  
  
## <a name="return-value"></a>Valeur de retour  
 En cas de réussite, retourne `S_OK`; sinon, retourne un code d’erreur.  
  
## <a name="remarks"></a>Remarques  
 Est de l’utilisation recommandée de cette méthode pour récupérer tous les octets de données dans un tableau local, car il n’existe aucun moyen d’ignorer les octets dans le processus de récupération. Dans ce cas, le paramètre `dataSize` doit être la valeur retournée par la [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) (méthode).  
  
## <a name="see-also"></a>Voir aussi  
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)   
 [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)