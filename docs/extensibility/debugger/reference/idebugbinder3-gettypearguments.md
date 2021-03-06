---
title: IDebugBinder3::GetTypeArguments | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugBinder3::GetTypeArguments
helpviewer_keywords: IDebugBinder3::GetTypeArguments method
ms.assetid: fa0c37a7-327f-463e-9a9d-bb3f534584cb
caps.latest.revision: "7"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7aff11599f00ad417915c4cb4f4e6ad907b5660d
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
Cette méthode récupère une liste de types d’arguments associé à cet objet.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetTypeArguments(  
   UINT          skip,  
   UINT          count,  
   IDebugField** ppFields,  
   UINT*         pFetched  
);  
```  
  
```csharp  
int GetTypeArguments(  
   uint          skip,  
   uint          count,  
   IDebugField[] ppFields,  
   out uint      pFetched  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `skip`  
 [in] Nombre de champs à ignorer avant d’obtenir les types d’arguments.  
  
 `count`  
 [in] Le nombre de champs argument à retourner (spécifie également la taille de la `ppFields` tableau).  
  
 `ppFields`  
 [dans, out] Tableau des champs qui seront remplies au retour de cette méthode.  
  
 `pFetched`  
 [out] \(facultatif) Le nombre d’arguments de type champs retournés.  
  
## <a name="return-value"></a>Valeur de retour  
 En cas de réussite, retourne `S_OK`; sinon, retourne un code d’erreur.  
  
## <a name="remarks"></a>Remarques  
 Le nombre de types d’arguments peut être obtenu au préalable avec [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md).  
  
## <a name="see-also"></a>Voir aussi  
 [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)   
 [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)