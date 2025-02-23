---
title: "CA1034: Nested types should not be visible"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "NestedTypesShouldNotBeVisible"
  - "CA1034"
helpviewer_keywords:
  - "NestedTypesShouldNotBeVisible"
  - "CA1034"
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
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
# CA1034: Nested types should not be visible

|||
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|Category|Microsoft.Design|
|Breaking Change|Breaking|

## Cause

An externally visible type contains an externally visible type declaration. Nested enumerations and protected types are exempt from this rule.

## Rule description
A nested type is a type declared within the scope of another type. Nested types are useful for encapsulating private implementation details of the containing type. Used for this purpose, nested types should not be externally visible.

Do not use externally visible nested types for logical grouping or to avoid name collisions; instead, use namespaces.

Nested types include the notion of member accessibility, which some programmers do not understand clearly.

Protected types can be used in subclasses and nested types in advance customization scenarios.

## How to fix violations
If you do not intend the nested type to be externally visible, change the type's accessibility. Otherwise, remove the nested type from its parent. If the purpose of the nesting is to categorize the nested type, use a namespace to create the hierarchy instead.

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The following example shows a type that violates the rule.

[!code-cpp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CPP/ca1034-nested-types-should-not-be-visible_1.cpp)]
[!code-csharp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CSharp/ca1034-nested-types-should-not-be-visible_1.cs)]
[!code-vb[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/VisualBasic/ca1034-nested-types-should-not-be-visible_1.vb)]