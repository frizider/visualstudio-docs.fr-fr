---
title: 'CA1018: Mark attributes with AttributeUsageAttribute | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 17
author: stevehoag
ms.author: shoag
manager: wpickett
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 0dc155a883bc474198df5c7b489335c056fe248f
ms.contentlocale: fr-fr
ms.lasthandoff: 08/30/2017

---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018: Mark attributes with AttributeUsageAttribute
|||  
|-|-|  
|TypeName|MarkAttributesWithAttributeUsage|  
|CheckId|CA1018|  
|Category|Microsoft.Design|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 The <xref:System.AttributeUsageAttribute?displayProperty=fullName> attribute is not present on the custom attribute.  
  
## <a name="rule-description"></a>Rule Description  
 When you define a custom attribute, mark it by using <xref:System.AttributeUsageAttribute> to indicate where in the source code the custom attribute can be applied. The meaning and intended usage of an attribute will determine its valid locations in code. For example, you might define an attribute that identifies the person who is responsible for maintaining and enhancing each type in a library, and that responsibility is always assigned at the type level. In this case, compilers should enable the attribute on classes, enumerations, and interfaces, but should not enable it on methods, events, or properties. Organizational policies and procedures would dictate whether the attribute should be enabled on assemblies.  
  
 The <xref:System.AttributeTargets?displayProperty=fullName> enumeration defines the targets that you can specify for a custom attribute. If you omit <xref:System.AttributeUsageAttribute>, your custom attribute will be valid for all targets, as defined by the `All` value of <xref:System.AttributeTargets> enumeration.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, specify targets for the attribute by using <xref:System.AttributeUsageAttribute>. See the following example.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 You should fix a violation of this rule instead of excluding the message. Even if the attribute inherits <xref:System.AttributeUsageAttribute>, the attribute should be present to simplify code maintenance.  
  
## <a name="example"></a>Example  
 The following example defines two attributes. `BadCodeMaintainerAttribute` incorrectly omits the <xref:System.AttributeUsageAttribute> statement, and `GoodCodeMaintainerAttribute` correctly implements the attribute that is described earlier in this section. Note that the property `DeveloperName` is required by the design rule [CA1019: Define accessors for attribute arguments](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) and is included for completeness.  
  
 [!code-csharp[FxCop.Design.AttributeUsage#1](../code-quality/codesnippet/CSharp/ca1018-mark-attributes-with-attributeusageattribute_1.cs)] [!code-vb[FxCop.Design.AttributeUsage#1](../code-quality/codesnippet/VisualBasic/ca1018-mark-attributes-with-attributeusageattribute_1.vb)]  
  
## <a name="related-rules"></a>Related Rules  
 [CA1019: Define accessors for attribute arguments](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)  
  
 [CA1813: Avoid unsealed attributes](../code-quality/ca1813-avoid-unsealed-attributes.md)  
  
## <a name="see-also"></a>See Also  
 [Attributes](/dotnet/standard/design-guidelines/attributes)