# Repository Standards

This document describes the standards to be applied when managing this code repository.

## Directory structure

When managing files in this repository, the following directory structure should be applied.

```text
.
├───.github                   # GitHub automation and copilot main instruction files
├───docs                      # Documentation root directory
├───infra                     # Infrastructure code (e.g. Bicep, Terraform, Pulumi)
├───samples                   # Sample code (if any)
├───src                       # Functional source code root directory
└───test                      # Test source code root directory
```

## EditorConfig Files

This section describes EditorConfig files and how they are used in this repository.

### What is EditorConfig?

The following description was taken from the official [EditorConfig website][official-editor-config-site]. You can find more details, including the official specification for EditorConfig on that site.

EditorConfig helps maintain consistent coding styles for multiple developers working on the same project across various [editors and IDEs][supported-ides]. The EditorConfig project consists of a file format for defining coding styles and a collection of text editor plugins that enable editors to read the file format and adhere to defined styles. EditorConfig files are easily readable and they work nicely with version control systems.

### Where are the EditorConfig files stored?

EditorConfig plugins search for `.editorconfig` files in the current file's directory and all parent directories, stopping when reaching the root filepath or finding a file with `root=true`. Files are processed top to bottom with more recent rules taking precedence - properties from closer files override those from more distant ones.

This repository includes a root `.editorconfig` file with recommended settings for all projects. To modify code styles:

1. **For repository-wide changes**: Edit the root `.editorconfig` file directly.
2. **For complete project-specific overrides**: Add a `.editorconfig` file in the project directory with `root = true` setting to ignore the repository root file.
3. **For partial project-specific overrides**: Add a `.editorconfig` file in the project directory without the `root = true` setting, including only the rules you want to override.

## Commit Messages

All commit messages should use the Conventional Commits standards laid out in [docs/development/02-conventional-commits.md][conventional-commits].

[official-editor-config-site]: https://editorconfig.org/
[supported-ides]: https://editorconfig.org/#pre-installed
[conventional-commits]: 02-conventional-commits.md
