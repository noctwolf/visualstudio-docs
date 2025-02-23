---
title: "CA1048: Do not declare virtual members in sealed types"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "DoNotDeclareVirtualMembersInSealedTypes"
  - "CA1048"
helpviewer_keywords:
  - "DoNotDeclareVirtualMembersInSealedTypes"
  - "CA1048"
ms.assetid: 5dcf4a30-6f98-48a8-b8cc-7b89ea757262
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1048: Do not declare virtual members in sealed types

|||
|-|-|
|TypeName|DoNotDeclareVirtualMembersInSealedTypes|
|CheckId|CA1048|
|Category|Microsoft.Design|
|Breaking Change|Breaking|

## Cause
A public type is sealed and declares a method that is both `virtual` (`Overridable` in Visual Basic) and not final. This rule does not report violations for delegate types, which must follow this pattern.

## Rule description
Types declare methods as virtual so that inheriting types can override the implementation of the virtual method. By definition, you cannot inherit from a sealed type, making a virtual method on a sealed type meaningless.

The Visual Basic and C# compilers do not allow types to violate this rule.

## How to fix violations
To fix a violation of this rule, make the method non-virtual or make the type inheritable.

## When to suppress warnings
Do not suppress a warning from this rule. Leaving the type in its current state can cause maintenance issues and does not provide any benefits.

## Example
The following example shows a type that violates this rule.

[!code-cpp[FxCop.Design.SealedVirtual#1](../code-quality/codesnippet/CPP/ca1048-do-not-declare-virtual-members-in-sealed-types_1.cpp)]