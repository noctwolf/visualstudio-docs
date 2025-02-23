---
title: "CA1408: Do not use AutoDual ClassInterfaceType"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "DoNotUseAutoDualClassInterfaceType"
  - "CA1408"
helpviewer_keywords:
  - "CA1408"
  - "DoNotUseAutoDualClassInterfaceType"
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1408: Do not use AutoDual ClassInterfaceType

|||
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|Category|Microsoft.Interoperability|
|Breaking Change|Breaking|

## Cause
A Component Object Model (COM) visible type is marked with the <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> attribute set to the `AutoDual` value of <xref:System.Runtime.InteropServices.ClassInterfaceType>.

## Rule description
Types that use a dual interface enable clients to bind to a specific interface layout. Any changes in a future version to the layout of the type or any base types will break COM clients that bind to the interface. By default, if the <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> attribute is not specified, a dispatch-only interface is used.

Unless marked otherwise, all public nongeneric types are visible to COM; all nonpublic and generic types are invisible to COM.

## How to fix violations
To fix a violation of this rule, change the value of the <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> attribute to the `None` value of <xref:System.Runtime.InteropServices.ClassInterfaceType> and explicitly define the interface.

## When to suppress warnings
Do not suppress a warning from this rule unless it is certain that the layout of the type and its base types will not change in a future version.

## Example
The following example shows a class that violates the rule and a re-declaration of the class to use an explicit interface.

[!code-csharp[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/CSharp/ca1408-do-not-use-autodual-classinterfacetype_1.cs)]
[!code-vb[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/VisualBasic/ca1408-do-not-use-autodual-classinterfacetype_1.vb)]

## Related rules
[CA1403: Auto layout types should not be COM visible](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

[CA1412: Mark ComSource Interfaces as IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## See also

- [Qualifying .NET Types for Interoperation](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [Interoperating with Unmanaged Code](/dotnet/framework/interop/index)