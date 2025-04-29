# General Code Guidelines

This document describes the coding guidelines to be applied to this project.

## Overview and Sources

These coding guidelines are designed to ensure consistency and maintainability across the codebase. They are sourced from the following locations.

- The [Microsoft Common C# code conventions document][coding-conventions]
- The [IDesign C# Coding Standard][idesign-csharp-standard]
- The [Ode to Code .NET Core Opinion Blog Series][ode-to-code]

## .NET Solution Structure

- The .NET solution file should be located in the root of the `src` directory
- Each functional code project should be located in its own directory under the `src` directory
- Each test code project should be located in its own directory under the `test` directory.

### File Organization

- Each C# project file (`.csproj`) should be located in the root of the corresponding project directory.
- One class per file
- File names match class names
- Logical folder structure
- Clear and nonconflicting namespaces
- As much as possible, directories under the root project directory should reflect the namespace hierarchy

## General Coding Principles

- SOLID principles
- DRY (Don't repeat yourself) as much as possible
- KISS (Keep it simple)
- Use spaces for indentation with four spaces per level, unless it is a csproj file, then use two spaces per level.
- All public members require doc comments.

[coding-conventions]: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions
[idesign-csharp-standard]: https://www.idesign.net/Resources/Standards
[ode-to-code]: https://odetocode.com/blogs/scott/archive/2018/08/28/net-core-opinion-1-structuring-a-repository.aspx
