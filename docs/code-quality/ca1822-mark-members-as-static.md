---
title: "CA1822: Mark members as static"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "MarkMembersAsStatic"
  - "CA1822"
helpviewer_keywords:
  - "MarkMembersAsStatic"
  - "CA1822"
ms.assetid: 743f0af7-41d1-4852-8d97-af0688b31118
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1822: Mark members as static

|||
|-|-|
|TypeName|MarkMembersAsStatic|
|CheckId|CA1822|
|Category|Microsoft.Performance|
|Breaking Change|Non-breaking - If the member is not visible outside the assembly, regardless of the change you make. Non Breaking - If you just change the member to an instance member with the `this` keyword.<br /><br /> Breaking - If you change the member from an instance member to a static member and it is visible outside the assembly.|

## Cause
A member that does not access instance data is not marked as static (Shared in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).

## Rule description
Members that do not access instance data or call instance methods can be marked as static (Shared in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]). After you mark the methods as static, the compiler will emit nonvirtual call sites to these members. Emitting nonvirtual call sites will prevent a check at runtime for each call that makes sure that the current object pointer is non-null. This can achieve a measurable performance gain for performance-sensitive code. In some cases, the failure to access the current object instance represents a correctness issue.

## How to fix violations
Mark the member as static (or Shared in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) or use 'this'/'Me' in the method body, if appropriate.

## When to suppress warnings
It is safe to suppress a warning from this rule for previously shipped code for which the fix would be a breaking change.

## Related rules
[CA1811: Avoid uncalled private code](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812: Avoid uninstantiated internal classes](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1804: Remove unused locals](../code-quality/ca1804-remove-unused-locals.md)