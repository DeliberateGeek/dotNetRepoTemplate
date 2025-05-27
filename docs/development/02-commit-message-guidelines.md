# Commit Messsage Guidelines

This project uses the Conventional Commits specification for all Git commit messages. The specific implementaion is defined below in the remainder of this document.

## What is Conventional Commits?

The Conventional Commits specification is a lightweight convention on top of commit messages. It provides an easy set of rules for creating an explicit commit history; which makes it easier to write automated tools on top of. This convention dovetails with [Semantic Verion (SemVer)][semver], by describing the features, fixes, and breaking changes made in commit messages.

## Spec Summary

This code base uses a pragmatic Conventional Commits implementation based on the [Conventional Commits Full Public Spec V1.0][full-public-spec].

## Spec Implementation

This section defines the variation of Conventional Commits to be used in this project. The implementations below take precedence over the core specification.

1. Commit messages **MUST** be prefixed with a type, which consists of a noun (e.g. `FEAT`, `FIX`, etc.), followed by an **OPTIONAL** scope, **OPTIONAL** `!`, and **REQUIRED** terminal colon and space.
1. It is **REQUIRED** that all types be provided in **UPPERCASE** characters for readability.
1. All types **MUST** come from the list of [Approved Types][approved-types]
1. The type `FEAT` **MUST** be used when a commit adds a new feature to your application or library.
1. The type `FIX` **MUST** be used when a commit represents a bug fix for your application or library.
1. Breaking changes **MUST** be indicated in the type/scope prefix of a commit by a `!` immediately before the `:`.
1. A scope **MAY** be provided after a type. A scope **MUST** consist of one of either of the following options:
   - A noun describing a section of the codebase surrounded by parenthesis (e.g. `FIX(parser):`).
   - A code representing a user story, bug, or issue captured in a work managing system such as Jira, Github, etc (e.g. `CHORE(story-167):`).
1. A scope **MAY** contain compound nouns for increaed readability and clarity. If a compound noun is used in a scope, the scope's token **MUST** use `-` in place of whitespace characters (e.g. `command-parser`). This helps readability and automation.
1. A scope **MAY** consist of **UPPERCASE** or **LOWERCASE** characters. If a list of approved scopes has been defined, a scope **MUST** come from the list of [Approved Scopes][approved-scopes].
1. A description **MUST** immediately follow the colon and space after the type/scope prefix. The description is a short summary of the code changes (e.g. `fix: array parsing issue when multiple spaces were contained in string`).
1. If a breaking change is indicated in the type/scope prefix, the commit description **MUST** describe the breaking change.
1. A longer commit body **MAY** be provided after the short description, providing additional contextual information about the code changes. The body **MUST** begin one blank line after the description.
1. A commit body is free-form and **MAY** consist of any number of newline separated paragraphs.
1. One or more footers **MAY** be provided one blank line after the body. Each footer **MUST** consist of a word token, followed by a `:<space>` separator, followed by a string value (this is inspired by the [got trailer convention][git-trailer]).
1. A footer’s token **MUST** use `-` in place of whitespace characters (e.g. `Approved-by`). This helps differentiate the footer section from a multi-paragraph body.
1. A footer’s value **MAY** contain spaces and newlines, and parsing **MUST** terminate when the next valid footer token/separator pair is observed.

## Approved Types

The following list is intended to be a primary starting point for approved types on a project. It is intended to be relatively generic and comprehensive. If this list is modified for a project it may require modification of the config files provided in the accelerator, particularly the configuration for the `LINTER` and `GITVERSION` configurations to support those changes. This indroductory text should be modified to indicate whether the Approved Types in this definition have been finalized for the project using this template.

### Approved Type List

| Type | Description |
| ---- | ----        |
| BUILD | Changes that affect the build system or external dependencies |
| CI | Changes to the CI configuration |
| DOCS | Changes only to documentation |
| FEAT | Denotes a new feature additon |
| FIX | Denotes a bug fix |
| MERGE | Denotes a merge commit |
| PERF | A code change that improves performance |
| REFACTOR | A code change that neither fixes a bu0g nor adds a feature |
| STYLE | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) |
| TEST | Adding missing tests or correcting existing tests |
| WIP | Denotes a work in progress commit - Often used inside a feature branch for interim commits - If the project uses squashed merge commits for Pull Requests, these will often be squashed in the PR |

## Approved Scopes

If scopes are being implemented in this project, this text should be updated to reflect the requirements for using scopes and what scopes are approved.

### Approved Scope Sample List

The following list represents a sample of potential approved scopes. It should be updated or removed based on the project needs.

| Scope | Description |
| ---- | ---- |
| UI | Denotes a code change made in the user interface layer of the system |
| API | Denotes a code change made in the API layer of the system |
| Retrieve new employee | Denotes a code change in the `retrieve new employee` feature of the system |
| Allocate inventory | Denotes a code change in the `allocate inventory` feature of the system |
| parser | Denotes a code change in the `parser` module of the system |

[semver]: http://semver.org/
[full-public-spec]: https://www.conventionalcommits.org/en/v1.0.0/#specification
[approved-types]: #approved-types
[approved-scopes]: #approved-scopes
[git-trailer]: https://git-scm.com/docs/git-interpret-trailers
