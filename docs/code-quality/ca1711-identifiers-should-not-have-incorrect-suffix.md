---
title: "CA1711: Identifiers should not have incorrect suffix"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1711"
  - "IdentifiersShouldNotHaveIncorrectSuffix"
helpviewer_keywords:
  - "CA1711"
  - "IdentifiersShouldNotHaveIncorrectSuffix"
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1711: Identifiers should not have incorrect suffix

|||
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|Category|Microsoft.Naming|
|Breaking Change|Breaking|

## Cause

An identifier has an incorrect suffix.

By default, this rule only looks at externally visible identifiers, but this is [configurable](#configurability).

## Rule description

By convention, only the names of types that extend certain base types or that implement certain interfaces, or types derived from these types, should end with specific reserved suffixes. Other type names should not use these reserved suffixes.

The following table lists the reserved suffixes and the base types and interfaces with which they are associated.

|Suffix|Base type/Interface|
|------------|--------------------------|
|Attribute|<xref:System.Attribute?displayProperty=fullName>|
|Collection|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|Dictionary|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|An event-handler delegate|
|Exception|<xref:System.Exception?displayProperty=fullName>|
|Permission|<xref:System.Security.IPermission?displayProperty=fullName>|
|Queue|<xref:System.Collections.Queue?displayProperty=fullName>|
|Stack|<xref:System.Collections.Stack?displayProperty=fullName>|
|Stream|<xref:System.IO.Stream?displayProperty=fullName>|

In addition, the following suffixes should **not** be used:

- `Delegate`

- `Enum`

- `Impl` (use `Core` instead)

- `Ex` or similar suffix to distinguish it from an earlier version of the same type

Naming conventions provide a common look for libraries that target the common language runtime. This reduces the learning curve that is required for new software libraries, and increases customer confidence that the library was developed by someone who has expertise in developing managed code.

## How to fix violations

Remove the suffix from the type name.

## When to suppress warnings

Do not suppress a warning from this rule unless the suffix has an unambiguous meaning in the application domain.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1711.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Naming). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Related rules

- [CA1710: Identifiers should have correct suffix](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## See also

- [Attributes](/dotnet/standard/design-guidelines/attributes)
- [Handling and raising events](/dotnet/standard/events/index)