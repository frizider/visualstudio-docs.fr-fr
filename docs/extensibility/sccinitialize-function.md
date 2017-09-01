---
title: SccInitialize Function | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
caps.latest.revision: 14
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
ms.openlocfilehash: 76235f932ccaac04672e50f8d349ab6fcd55cd4d
ms.contentlocale: fr-fr
ms.lasthandoff: 08/28/2017

---
# <a name="sccinitialize-function"></a>SccInitialize Function
This function initializes the source control plug-in and provides capabilities and limits to the integrated development environment (IDE).  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
SCCRTN SccInitialize (  
   LPVOID* ppvContext,  
   HWND    hWnd,  
   LPCSTR  lpCallerName,  
   LPSTR   lpSccName,  
   LPLONG  lpSccCaps,  
   LPSTR   lpAuxPathLabel,  
   LPLONG  pnCheckoutCommentLen,  
   LPLONG  pnCommentLen  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppvContext`  
 [in] The source control plug-in can place a pointer to its context structure here.  
  
 `hWnd`  
 [in] A handle to the IDE window that the source control plug-in can use as a parent for any dialog boxes that it provides.  
  
 `lpCallerName`  
 [in] The name of the program calling the source control plug-in.  
  
 `lpSccName`  
 [in, out] The buffer where the source control plug-in puts its own name (not to exceed `SCC_NAME_LEN`).  
  
 `lpSccCaps`  
 [out] Returns the source control plug-in's capability flags.  
  
 `lpAuxPathLabel`  
 [in, out] The buffer where the source control plug-in puts a string that describes the `lpAuxProjPath` parameter returned by the [SccOpenProject](../extensibility/sccopenproject-function.md) and the [SccGetProjPath](../extensibility/sccgetprojpath-function.md) (not to exceed `SCC_AUXLABEL_LEN`).  
  
 `pnCheckoutCommentLen`  
 [out] Returns the maximum permissible length for a checkout comment.  
  
 `pnCommentLen`  
 [out] Returns the maximum permissible length for other comments.  
  
## <a name="return-value"></a>Return Value  
 The source control plug-in implementation of this function is expected to return one of the following values:  
  
|Value|Description|  
|-----------|-----------------|  
|SCC_OK|Source control initialization succeeded.|  
|SCC_E_INITIALIZEFAILED|System could not be initialized.|  
|SCC_E_NOTAUTHORIZED|The user is not allowed to perform the specified operation.|  
|SCC_E_NONSPECFICERROR|Nonspecific failure; source control system was not initialized.|  
  
## <a name="remarks"></a>Remarks  
 The IDE calls this function when it first loads the source control plug-in. It enables the IDE to pass certain information, such as the caller name, to the plug-in. The IDE also gets back certain information such as the maximum allowable length for comments and the plug-in's capabilities.  
  
 The `ppvContext` points to a `NULL` pointer. The source control plug-in can allocate a structure for its own use and store a pointer to that structure in `ppvContext`. The IDE will pass this pointer to every other VSSCI API function, allowing the plug-in to have context information available without resorting to global storage and to support multiple instances of the plug-in. This structure should be deallocated when the [SccUninitialize](../extensibility/sccuninitialize-function.md) is called.  
  
 The `lpCallerName` and `lpSccName` parameters enable the IDE and the source control plug-in to exchange names. These names may be used simply to distinguish among multiple instances, or they may actually appear in menus or dialog boxes.  
  
 The `lpAuxPathLabel` parameter is a string used as a comment to identify the auxiliary project path that is stored in the solution file and passed to the source control plug-in in a call to the [SccOpenProject](../extensibility/sccopenproject-function.md). [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] uses the string "SourceSafe Project:"; other source control plug-ins should refrain from using this particular string.  
  
 The `lpSccCaps` parameter gives the source control plug-in a place to store bitflags indicating the plug-in's capabilities. (For a full list of capability bitflags, see [Capability Flags](../extensibility/capability-flags.md)). For instance, if the plug-in plans to write results into a caller-provided callback function, the plug-in would set the capability bit SCC_CAP_TEXTOUT. This would signal the IDE to create a window for version control results.  
  
## <a name="see-also"></a>See Also  
 [Source Control Plug-in API Functions](../extensibility/source-control-plug-in-api-functions.md)   
 [SccUninitialize](../extensibility/sccuninitialize-function.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)   
 [Capability Flags](../extensibility/capability-flags.md)