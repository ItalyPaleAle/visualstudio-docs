---
title: "CA1802: Use Literals Where Appropriate"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "UseLiteralsWhereAppropriate"
  - "CA1802"
helpviewer_keywords:
  - "UseLiteralsWhereAppropriate"
  - "CA1802"
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1802: Use Literals Where Appropriate

|||
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|Category|Microsoft.Performance|
|Breaking Change|Non-breaking|

## Cause

A field is declared `static` and `readonly` (`Shared` and `ReadOnly` in Visual Basic), and is initialized with a value that is computable at compile time.

By default, this rule only looks at externally visible fields, but this is [configurable](#configurability).

## Rule description

The value of a `static readonly` field is computed at runtime when the static constructor for the declaring type is called. If the `static readonly` field is initialized when it is declared and a static constructor is not declared explicitly, the compiler emits a static constructor to initialize the field.

The value of a `const` field is computed at compile time and stored in the metadata, which increases runtime performance when it is compared to a `static readonly` field.

Because the value assigned to the targeted field is computable at compile time, change the declaration to a `const` field so that the value is computed at compile time instead of at runtime.

## How to fix violations

To fix a violation of this rule, replace the `static` and `readonly` modifiers with the `const` modifier.

## When to suppress warnings

It is safe to suppress a warning from this rule, or disable the rule, if performance is not of concern.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1802.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Performance). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following example shows a type, `UseReadOnly`, that violates the rule and a type, `UseConstant`, that satisfies the rule.

[!code-vb[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/VisualBasic/ca1802-use-literals-where-appropriate_1.vb)]
[!code-csharp[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/CSharp/ca1802-use-literals-where-appropriate_1.cs)]