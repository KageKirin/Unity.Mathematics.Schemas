# Collaboration guide

This guide contains the collaboration guidelines to use
for contributing and maintening this project.

To assure future compatibility and ease of maintenance,
**these are to be observed as strictly as possible**.

## Code Formatting

This project relies on the automatic code formatting
provided by **[CSharpier](https://csharpier.com/)**.

### DO NOT USE ANY OTHER CODE FORMATTING TOOL UNDER ANY CIRCUMSTANCES

This assures consistency.

### ALWAYS RUN `CSHARPIER` OVER THE WHOLE PROJECT BEFORE COMMITTING

This assures that no wrong formatting gets committed.
It also assures that the code is compilable.

## Commit Convention

This project follows the **[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)** guidelines,
along with the **[Angular Commit](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)** recommentations.

### Change types

* `build`: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
* `ci`: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
* `docs`: Documentation only changes
* `feat`: A new feature
* `fix`: A bug fix
* `perf`: A code change that improves performance
* `refactor`: A code change that neither fixes a bug nor adds a feature
* `repo` A change pertaining to repository configuration (submodule, gitignore, gitattributes, ...).
* `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* `test`: Adding missing tests or correcting existing tests

### Scopes

* `build` => filename where change occurred (without path)
* `ci` => workflow name where change occurred
* `docs` => stem of filename where change occurred (e.g. `README` without the `.md`)
* `feat`, `fix`, `perf`, `refactor` => file or module where changes occurred
* `style` => filename or project (also, use sparingly (no need for n single-file commits)
  and prefer rebasing to integrate style changes with the actual feature changes)
* `repo` => filename without leading `.` (`gitignore`)
* `test` => project where change occurred (without path)

### PR titles

Use the same **Conventional Commits** format with the best-fitting scope.

## Language convention

**Only grammatically and orthographically correct US English is allowed.**
In case of doubt for wording and spelling, check an online thesaurus and dictionary.

## Line endings

### DO NOT CHANGE LINE ENDINGS

CSharpier restores the correct line endings anyway.

## UTF-8

**UTF-8 NO BOM** is set by CSharpier and must not be altered.

## Pull Requests

### SQUASH-MERGING only

Rationale: when used with Atomic PRs, squash-merges have the advantage of hiding the development details
(of which there should be few) and thus allowing easier rebases.

### ATOMIC PRs

PRs must only contain the minimum amount of changes required for the purpose set by the PR title.

### CI MUST PASS

Needless to say that a PR that fails CI checks **MUST NOT BE MERGED UNDER ANY CIRCUMSTANCES**.
