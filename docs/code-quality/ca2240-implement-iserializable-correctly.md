---
title: "CA2240: Implement ISerializable correctly"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA2240"
  - "ImplementISerializableCorrectly"
helpviewer_keywords:
  - "CA2240"
  - "ImplementISerializableCorrectly"
ms.assetid: cf05936d-0d6c-49ed-a1b4-220032e50b97
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA2240: Implement ISerializable correctly

|||
|-|-|
|TypeName|ImplementISerializableCorrectly|
|CheckId|CA2240|
|Category|Microsoft.Usage|
|Breaking Change|Non Breaking|

## Cause

An externally visible type is assignable to the <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface and one of the following conditions is true:

- The type inherits but does not override the <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> method and the type declares instance fields that are not marked with the <xref:System.NonSerializedAttribute?displayProperty=fullName> attribute.

- The type is not sealed and the type implements a <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> method that is not externally visible and overridable.

## Rule description
Instance fields that are declared in a type that inherits the <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface are not automatically included in the serialization process. To include the fields, the type must implement the <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> method and the serialization constructor. If the fields should not be serialized, apply the <xref:System.NonSerializedAttribute> attribute to the fields to explicitly indicate the decision.

In types that are not sealed, implementations of the <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> method should be externally visible. Therefore, the method can be called by derived types, and is overridable.

## How to fix violations
To fix a violation of this rule, make the <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> method visible and overridable and make sure all instance fields are included in the serialization process or explicitly marked with the <xref:System.NonSerializedAttribute> attribute.

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The following example shows two serializable types that violate the rule.

[!code-csharp[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/CSharp/ca2240-implement-iserializable-correctly_1.cs)]
[!code-cpp[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/CPP/ca2240-implement-iserializable-correctly_1.cpp)]
[!code-vb[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/VisualBasic/ca2240-implement-iserializable-correctly_1.vb)]

## Example
The following example fixes the two previous violations by providing an overrideable implementation of <xref:System.Runtime.Serialization.ISerializable.GetObjectData> on the Book class and by providing an implementation of `GetObjectData` on the Library class.

[!code-cpp[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/CPP/ca2240-implement-iserializable-correctly_2.cpp)]
[!code-csharp[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/CSharp/ca2240-implement-iserializable-correctly_2.cs)]
[!code-vb[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/VisualBasic/ca2240-implement-iserializable-correctly_2.vb)]

## Related rules

- [CA2236: Call base class methods on ISerializable types](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)
- [CA2229: Implement serialization constructors](../code-quality/ca2229-implement-serialization-constructors.md)
- [CA2238: Implement serialization methods correctly](../code-quality/ca2238-implement-serialization-methods-correctly.md)
- [CA2235: Mark all non-serializable fields](../code-quality/ca2235-mark-all-non-serializable-fields.md)
- [CA2237: Mark ISerializable types with SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)
- [CA2239: Provide deserialization methods for optional fields](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)
- [CA2120: Secure serialization constructors](../code-quality/ca2120-secure-serialization-constructors.md)