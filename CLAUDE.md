# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

**Repository Type**: .NET Project Template
**Purpose**: Provides a starting point for new .NET solutions with pre-configured coding standards, documentation structure, and development guidelines.

**When Using This Template**: Customize this CLAUDE.md by:
1. Removing template-specific sections (this notice, FAQ template questions, etc.)
2. Adding actual project details (name, purpose, business context)
3. Updating Tech Stack section with real framework versions and dependencies
4. Adding project-specific architectural decisions and patterns
5. Including any project-specific development commands or workflows

### Communication Style
- Use friendly, informal tone (like a helpful colleague)
- Reference the comprehensive documentation in `docs/` as authoritative source
- When uncertain about requirements or implementation approaches, ask clarifying questions rather than making assumptions

## Repository Structure

```text
.
├── .github                   # GitHub automation and copilot instruction files
├── docs                      # Documentation root directory
│   ├── architecture          # Architecture decision records and diagrams
│   └── development           # Development guidelines and standards
├── src                       # Functional source code root directory
└── test                      # Test source code root directory (when added)
```

**Key Organizational Principles**:
- Solution file (`.sln`) located in root of `src` directory
- Each C# project in its own directory under appropriate root (`src` for functional, `test` for tests)
- Folder structure beneath each project matches namespace structure
- One class per file (unless partial classes required)
- File names match class names

## Common Development Commands

### Building
```bash
dotnet build                              # Build the solution
dotnet build --configuration Release      # Build for release
dotnet clean                              # Clean build artifacts
```

### Testing
```bash
dotnet test                                                          # Run all tests
dotnet test --filter "FullyQualifiedName~Namespace.ClassName"       # Run specific tests
dotnet test --collect:"XPlat Code Coverage"                         # Run tests with coverage
```

### Code Formatting
- EditorConfig rules enforced via `.editorconfig` in repository root
- Visual Studio and VS Code automatically apply formatting on save
- Project-specific overrides can be added in project directories (see EditorConfig section below)

## Tech Stack & Dependencies

**Target Framework**: [To be specified when creating project from template]
**Key Technologies**:
- .NET [version TBD]
- [Additional frameworks/libraries TBD]

**Important Notes**:
- This template uses EditorConfig for code formatting enforcement
- Conventional Commits with UPPERCASE types is mandatory
- All projects follow Microsoft C# coding conventions with specific customizations documented in `docs/development/`

## Commit Message Standards

This project uses **Conventional Commits** with specific requirements:

- Types **MUST** be in **UPPERCASE** (e.g., `FEAT`, `FIX`, `DOCS`, `REFACTOR`)
- Format: `TYPE(scope): description`
- Breaking changes indicated with `!` before the colon: `FEAT(api)!: breaking change`
- Scopes are optional but use lowercase or match approved list

**Example Commits**:
```
FEAT(auth): add JWT token validation
FIX(parser): resolve null reference in edge case handling
DOCS(readme): update installation instructions
REFACTOR(services): simplify dependency injection configuration
PERF(database): optimize query performance with indexes
```

### Approved Commit Types

| Type | Description |
| ---- | ----------- |
| BUILD | Changes to build system or dependencies |
| CI | Changes to CI configuration |
| DOCS | Documentation only changes |
| FEAT | New feature addition |
| FIX | Bug fix |
| MERGE | Merge commit |
| PERF | Performance improvement |
| REFACTOR | Code change that neither fixes bug nor adds feature |
| STYLE | Code style changes (formatting, whitespace, etc.) |
| TEST | Adding or correcting tests |
| WIP | Work in progress (often squashed in PRs) |

## C# Coding Guidelines

### Naming Conventions

- **PascalCase**: Classes, records, structs, interfaces (prefix with `I`), enums, public members, methods, type parameters (prefix with `T`)
- **camelCase**: Private/internal fields (prefix with `_`), parameters, local variables, primary constructor parameters on class/struct
- **ALL_CAPS**: Constants (with underscore between words)
- **Acronyms**: PascalCase for 3+ chars (`XmlParser`), UPPERCASE for 2 chars (`IOStream`)

**Examples of Key Conventions**:

**Private Fields with Underscore Prefix**:
```csharp
public class UserService
{
    private readonly IUserRepository _userRepository;  // ✅ Correct
    private readonly ILogger _logger;                  // ✅ Correct

    // private IUserRepository userRepository;         // ❌ Avoid
}
```

**Constants in ALL_CAPS**:
```csharp
public class ConfigurationKeys
{
    public const string DATABASE_CONNECTION_STRING = "DbConnection";  // ✅ Correct
    public const int MAX_RETRY_ATTEMPTS = 3;                         // ✅ Correct

    // public const string DatabaseConnection = "DbConnection";      // ❌ Avoid
}
```

### Language Style

- Use language keywords (`string`, `int`) not runtime types (`String`, `Int32`)
- Prefer modern C# features and async/await patterns
- Use LINQ method syntax over query syntax
- Use collection expressions: `string[] vowels = [ "a", "e", "i", "o", "u" ];`
- Use implicit typing (`var`) when type is obvious from right side
- Use `Func<>` and `Action<>` instead of custom delegates
- Prefer `using` declarations over `using` statements when intent is clear

### Code Layout

- **4 spaces** for indentation (except .csproj files use 2 spaces)
- **No tabs** except in .sln files (Visual Studio requirement)
- **Block-scoped namespaces** (not file-scoped)
- **`using` directives outside namespace**
- **Allman style braces** (opening brace on new line)
- One statement per line, one declaration per line
- Max line length: 120 characters

**Namespace Organization Example**:

Use block-scoped namespaces (not file-scoped) for clearer scope definition and visual separation:

✅ **Correct**:
```csharp
using System;
using Microsoft.Extensions.Logging;

namespace MyProject.Services
{
    public class UserService
    {
        // Implementation
    }
}
```

❌ **Avoid**:
```csharp
namespace MyProject.Services;  // File-scoped namespace - not used in this template

using System;                  // Using directives inside namespace - avoid
```

**Rationale**: Block-scoped namespaces provide clearer visual separation between namespace declarations and type definitions, and make it immediately obvious where the namespace scope begins and ends.

### Comments and Documentation

- Use single-line comments (`//`) not multi-line (`/* */`)
- Comments on separate lines, not at end of code lines
- Complete sentences with proper capitalization and punctuation
- One space after `//`
- Document "why" not "what" - code should be self-explanatory
- Use XML comments for public APIs (methods, classes, fields accessible outside solution)

### Exception Handling

- Only catch exceptions you can explicitly handle
- When rethrowing, use `throw;` to preserve stack trace
- Or throw new exception with original as inner exception to maintain context

### EditorConfig

- Root `.editorconfig` file contains repository-wide standards
- Project-specific overrides can be added in project directories:
  - With `root=true`: completely override root settings
  - Without `root=true`: partial override (only specified rules)

## Template Customization Checklist

When creating a new project from this template, update the following:

- [ ] Update this CLAUDE.md file:
  - [ ] Remove template-specific sections and notices
  - [ ] Add actual project name, purpose, and business context
  - [ ] Update Tech Stack section with real framework versions and dependencies
  - [ ] Add project-specific architectural decisions
  - [ ] Update Common Development Commands with project-specific commands
- [ ] Update `.github/copilot-instructions.md` with project-specific context
- [ ] Review and customize documentation in `docs/` directory:
  - [ ] Update or remove `docs/architecture/` content
  - [ ] Customize development guidelines as needed
  - [ ] Add project-specific documentation
- [ ] Update `.editorconfig` if project has different formatting requirements
- [ ] Customize Conventional Commits approved types/scopes if needed
- [ ] Remove this checklist section once customization is complete

## Frequently Asked Questions

**Q: This is a template - what should I customize?**
A: See the Template Customization Checklist above. At minimum: update Project Context, add specific tech stack details, and remove template-specific sections.

**Q: Why UPPERCASE commit types instead of lowercase?**
A: Repository standard for improved readability and automated tooling compatibility. The UPPERCASE convention makes commit types immediately visible when scanning git history.

**Q: Why use block-scoped namespaces instead of file-scoped?**
A: This template mandates block-scoped namespaces for clearer scope definition and visual separation between namespace declarations and type definitions. While file-scoped namespaces are a modern C# feature, block-scoped provides better visual structure for this template's conventions.

**Q: What if my project doesn't need all the documentation?**
A: Remove or simplify documentation sections as appropriate for your project needs, but maintain the core coding standards and commit message conventions.

**Q: Can I override the EditorConfig settings for my specific project?**
A: Yes. Add a `.editorconfig` file in your project directory. Use `root=true` for complete override, or omit it to only override specific rules while inheriting others from the repository root.

## Development Guidelines

### Code Principles

- Prefer clarity over brevity in naming
- Avoid abbreviations unless widely understood (`Http`, `Xml`)
- Use modern language features and C# versions
- Avoid overly complex logic - keep it simple (KISS principle)
- Follow security best practices (OWASP top 10)
- Optimize for readability and maintainability first, performance second (unless performance requirements dictate otherwise)

## Extended Documentation

### Imported Guidelines (Always Available)

The following documentation is imported and always available to Claude:

@docs/development/02-commit-message-guidelines.md

### Reference Documentation (Read When Needed)

For detailed guidelines on specific topics, reference these documents:
- `docs/development/01-repository-guidelines.md` - Repository structure and EditorConfig usage
- `docs/development/03-general-code-guidelines.md` - Comprehensive C# coding standards
- `docs/development/04-csharp-naming-guidelines.md` - Complete naming conventions with examples
- `docs/development/05-performance-guidelines.md` - Performance optimization patterns
- `docs/development/05-security-guidelines.md` - Security best practices and OWASP guidelines
