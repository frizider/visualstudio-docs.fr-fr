---
title: IDebugPortEx2::GetPortProcessId | Documents Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugPortEx2::GetPortProcessId
helpviewer_keywords: IDebugPortEx2::GetPortProcessId
ms.assetid: be85be66-47e6-415f-b0ca-24599aa5f13c
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 300f0553ee081dee8adc34ab48ce1989fc86e6c9
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="idebugportex2getportprocessid"></a>IDebugPortEx2::GetPortProcessId
Obtient l’ID de processus du port lui-même.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetPortProcessId (   
   DWORD* pdwProcessId  
);  
```  
  
```csharp  
int GetPortProcessId (   
   out uint pdwProcessId  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `pdwProcessId`  
 [out] Retourne l’ID du processus physique du port lui-même.  
  
## <a name="return-value"></a>Valeur de retour  
 En cas de réussite, retourne `S_OK`; sinon, retourne un code d’erreur.  
  
## <a name="remarks"></a>Remarques  
 Dans le runtime Win32, par exemple, cette méthode appelle généralement la fonction Win32 `GetCurrentProcessId` pour obtenir l’ID du processus physique.  
  
## <a name="see-also"></a>Voir aussi  
 [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)