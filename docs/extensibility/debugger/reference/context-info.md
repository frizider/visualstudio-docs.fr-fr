---
title: CONTEXT_INFO | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: MT
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 5cee396c4659807ca4dcded60f4d1f1fbbcc3f82
ms.contentlocale: fr-fr
ms.lasthandoff: 08/28/2017

---
# <a name="contextinfo"></a>CONTEXT_INFO
This structure describes a memory context or code context.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _tagCONTEXT_INFO {   
   CONTEXT_INFO_FIELDS dwFields;  
   BSTR                bstrModuleUrl;  
   BSTR                bstrFunction;  
   TEXT_POSITION       posFunctionOffset;  
   BSTR                bstrAddress;  
   BSTR                bstrAddressOffset;  
   BSTR                bstrAddressAbsolute;  
} CONTEXT_INFO;  
```  
  
```csharp  
public struct CONTEXT_INFO {  
   public uint          dwFields;  
   public string        bstrModuleUrl;  
   public string        bstrFunction;  
   public TEXT_POSITION posFunctionOffset;  
   public string        bstrAddress;  
   public string        bstrAddressOffset;  
   public string        bstrAddressAbsolute;  
};  
```  
  
## <a name="members"></a>Members  
 dwFields  
 A combination of flags from he [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md) enumeration that specifies which fields are filled out**.**  
  
 bstrModuleUrl  
 The name of the module where the context is located.  
  
 bstrFunction  
 The function name where the context is located.  
  
 posFunctionOffset  
 A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) structure that identifies the line and column offset of the function associated with the code context.  
  
 bstrAddress  
 The address in code where the given context is located.  
  
 bstrAddressOffset  
 The offset of the address in code where the given context is located.  
  
 bstrAddressAbsolute  
 The absolute address in memory where the given context is located.  
  
## <a name="remarks"></a>Remarks  
 This structure is returned from a call to the [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) method.  
  
 A typical use for this structure is in support of a **Memory** debug window.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)   
 [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)