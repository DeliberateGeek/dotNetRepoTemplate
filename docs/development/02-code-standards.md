# Code Standards

This document describes the coding standards to be applied to this project.

## Overview

These coding standards are designed to ensure consistency and maintainability across the codebase

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

## Coding Guidelines

### General Principles

- SOLID principles
- DRY (Don't repeat yourself) as much as possible
- KISS (Keep it simple)
- Use spaces for indentation with four spaces per level, unless it is a csproj file, then use two spaces per level.
- All public members require doc comments.

### C# Naming Conventions

Except where explicitly described in this section, use the conventions defined in the [Microsoft C# identifier naming rules and conventions document](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names).

- C# keyword names should be avoided when naming identifiers

### Coding Conventions

Except where explicitly described in this section, use the conventions defined in the [Microsoft Common C# code conventions document](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions`)
