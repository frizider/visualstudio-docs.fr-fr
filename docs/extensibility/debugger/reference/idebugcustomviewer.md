---
title: IDebugCustomViewer | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
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
ms.openlocfilehash: 74fcd4f2c5ac72aeede1acd407f8bfb97f18932d
ms.contentlocale: fr-fr
ms.lasthandoff: 08/28/2017

---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
This interface enables an expression evaluator (EE) to display a property's value in whatever format is necessary.  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugCustomViewer : IUknown  
```  
  
## <a name="notes-for-implementers"></a>Notes for Implementers  
 An EE implements this interface to display a property's value in a custom format.  
  
## <a name="notes-for-callers"></a>Notes for Callers  
 A call to COM's `CoCreateInstance` function instantiates this interface. The `CLSID` passed to `CoCreateInstance` is obtained from the registry. A call to [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) obtains the location in the registry. See Remarks for details as well as the Example.  
  
## <a name="methods-in-vtable-order"></a>Methods in Vtable Order  
 This interface implements the following method:  
  
|Method|Description|  
|------------|-----------------|  
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|Does whatever is necessary to display a given value.|  
  
## <a name="remarks"></a>Remarks  
 This interface is used when a property's value cannot be displayed by normal means—for example, with a data table or another complex property type. A custom viewer, as represented by the `IDebugCustomViewer` interface, is different from a type visualizer, which is an external program for displaying data of a specific type regardless of the EE. The EE implements a custom viewer that is specific to that EE. A user selects which type of visualizer to use, be it a type visualizer or a custom viewer. See [Visualizing and Viewing Data](../../../extensibility/debugger/visualizing-and-viewing-data.md) for details on this process.  
  
 A custom viewer is registered in the same way as an EE and, therefore, requires a language GUID and a vendor GUID. The exact metric (or registry entry name) is known only to the EE. This metric is returned in the [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) structure, which in turn is returned by a call to [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md). The value stored in the metric is the `CLSID` that is passed to COM's `CoCreateInstance` function (see the Example).  
  
 The [SDK Helpers for Debugging](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) function, `SetEEMetric`, can be used to register a custom viewer. See the "Expression Evaluators" registry section of `Debugging SDK Helpers` for the specific registry keys that a custom viewer needs. Note that a custom viewer needs only one metric (which is defined by the EE's implementer) whereas an expression evaluator requires several predefined metrics.  
  
 Normally, a custom viewer provides a read-only view of the data, since the [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) interface supplied to [DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) has no methods for changing the property's value except as a string. In order to support changing arbitrary blocks of data, the EE implements a custom interface on the same object that implements the `IDebugProperty3` interface. This custom interface would then provide the methods needed to change an arbitrary block of data.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>Example  
 This example shows how to get the first custom viewer from a property if that property has any custom viewers.  
  
```cpp  
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)  
{  
    // This string is typically defined globally.  For this example, it  
    // is defined here.  
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";  
    IDebugCustomViewer *pViewer = NULL;  
    if (pProperty != NULL) {  
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);  
        if (pProperty3 != NULL) {  
            HRESULT hr;  
            ULONG viewerCount = 0;  
            hr = pProperty3->GetCustomViewerCount(&viewerCount);  
            if (viewerCount > 0) {  
                ULONG viewersFetched = 0;  
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };  
                hr = pProperty3->GetCustomViewerList(0,  
                                                     1,  
                                                     &viewerInfo,  
                                                     &viewersFetched);  
                if (viewersFetched == 1) {  
                    CLSID clsidViewer = { 0 };  
                    CComPtr<IDebugCustomViewer> spCustomViewer;  
                    // Get the viewer's CLSID from the registry.  
                    ::GetEEMetric(viewerInfo.guidLang,  
                                  viewerInfo.guidVendor,  
                                  viewerInfo.bstrMetric,  
                                  &clsidViewer,  
                                  strRegistrationRoot);  
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {  
                        // Instantiate the custom viewer.  
                        spCustomViewer.CoCreateInstance(clsidViewer);  
                        if (spCustomViewer != NULL) {  
                            pViewer = spCustomViewer.Detach();  
                        }  
                    }  
                }  
            }  
        }  
    }  
    return(pViewer);  
}  
```  
  
## <a name="see-also"></a>See Also  
 [Core Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [SDK Helpers for Debugging](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)