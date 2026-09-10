# Contributing to Roamly Android

Thank you for contributing to **Roamly Android**.

This document defines the development workflow, branch naming rules, commit message convention, pull request process, and basic code-quality expectations for this repository.

The goal is to keep the project history clean and make collaboration across the Roamly repositories predictable.

---

## Repository

**Repository:** `roamly-android`

**Main branch:** `main`

Do not develop features directly on `main`. Create a separate branch for every feature, fix, refactor, or maintenance task.

---

## Git Workflow

Use this workflow for normal development:

```bash
# 1. Switch to main
git switch main

# 2. Get the latest changes
git pull origin main

# 3. Create a new branch
git switch -c <branch-name>

# 4. Make your changes

# 5. Check changed files
git status

# 6. Stage the changes
git add .

# 7. Commit
git commit -m "<type>: <short description>"

# 8. Push the branch
git push -u origin <branch-name>
```

After pushing, open a Pull Request from your branch into `main`.

---

## Branch Naming Convention

Use lowercase names and separate words with hyphens.

| Type | Format | Example |
|---|---|---|
| Feature | `feature/<name>` | `feature/trip-details` |
| Bug fix | `fix/<name>` | `fix/login-validation` |
| Refactor | `refactor/<name>` | `refactor/trip-repository` |
| Chore | `chore/<name>` | `chore/update-dependencies` |
| Documentation | `docs/<name>` | `docs/update-readme` |
| Tests | `test/<name>` | `test/trip-service` |

### Good examples

```text
feature/create-trip
feature/authentication
fix/profile-image-loading
refactor/network-layer
chore/update-dependencies
docs/api-documentation
test/trip-repository
```

### Avoid

```text
new-branch
my-branch
test123
trip-stuff
changes
final-version
```

---

## Commit Message Convention

Roamly uses a simplified **Conventional Commits** style.

Format:

```text
<type>: <short description>
```

Allowed commit types:

| Type | Use for |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `refactor` | Code restructuring without changing behavior |
| `chore` | Tooling, configuration, dependency, or maintenance work |
| `docs` | Documentation only |
| `test` | Adding or updating tests |
| `style` | Formatting or style-only changes |
| `perf` | Performance improvements |

### Examples

```text
feat: add trip creation flow
fix: handle empty destination response
refactor: simplify authentication repository
chore: update project dependencies
docs: add setup instructions
test: add trip repository tests
```

Keep commit messages:

- Short and clear.
- Written in the imperative style.
- Focused on one logical change.
- Lowercase after the colon unless a proper noun requires capitalization.

Avoid messages such as:

```text
update
changes
fix stuff
final
done
new code
```

---

## Keeping Your Branch Updated

Before opening or updating a Pull Request, bring the latest `main` changes into your branch.

Preferred approach:

```bash
git switch main
git pull origin main

git switch <your-branch>
git merge main
```

If conflicts occur:

1. Resolve each conflict carefully.
2. Verify that both your changes and the required `main` changes are preserved.
3. Stage the resolved files:

```bash
git add .
```

4. Complete the merge:

```bash
git commit
```

5. Push the branch:

```bash
git push
```

Do not blindly accept all changes from one side when resolving conflicts. Review the final code before committing.

---

## Pull Request Guidelines

Before creating a Pull Request:

- Make sure the project builds successfully.
- Run relevant tests.
- Remove debugging code, temporary comments, and unused files.
- Check that no secrets or credentials are committed.
- Update documentation when behavior or setup changes.
- Confirm the branch contains only changes related to the task.

### Pull Request title

Use the same style as commit messages:

```text
feat: add trip creation flow
fix: handle failed login response
refactor: improve network layer
```

### Pull Request description

Include:

```markdown
## What changed?
Briefly describe the implementation.

## Why?
Explain why the change was needed.

## How was it tested?
Describe the tests or manual checks performed.

## Screenshots
Add screenshots for UI changes when applicable.
```

---

## Code Review

A Pull Request should be reviewed before it is merged when working with other contributors.

Reviewers should check:

- Correctness.
- Readability.
- Architecture consistency.
- Error handling.
- Naming.
- Tests.
- Security concerns.
- Unnecessary duplication.
- UI consistency, when applicable.

Do not merge a Pull Request with unresolved review comments.

---

## Secrets and Sensitive Files

Never commit:

- API keys.
- Access tokens.
- Passwords.
- Private certificates.
- Production credentials.
- Local environment files containing secrets.

Store local secrets in ignored configuration files or environment variables.

Before committing, always check:

```bash
git status
git diff --staged
```


## Android Development Guidelines

This repository contains the native **Roamly Android** application.

Follow the existing Kotlin, Jetpack Compose, architecture, dependency-injection, and navigation conventions.

### Setup

Open the project in Android Studio and allow Gradle to sync.

From the repository root, common verification commands are:

```bash
./gradlew build
./gradlew test
```

Run additional lint or instrumentation tests when configured by the project.

### Kotlin and Jetpack Compose conventions

- Follow Kotlin naming conventions.
- Keep composables focused on UI.
- Keep business logic in ViewModels/use cases rather than composables.
- Prefer immutable UI state.
- Follow the existing unidirectional data-flow pattern.
- Reuse shared Compose components.
- Handle loading, empty, success, and failure states.
- Avoid hardcoded reusable colors, typography, spacing, and strings.
- Keep navigation consistent with the application's existing navigation setup.
- Use coroutines safely and avoid unnecessary work on the main thread.

### New feature structure

Follow the repository's existing architecture. A feature may use a structure similar to:

```text
feature/
└── trips/
    ├── data/
    ├── domain/
    └── presentation/
```

Do not introduce a different architecture for a single feature without a project-level decision.

### Testing

Before opening a Pull Request:

- Build the application successfully.
- Run relevant unit tests.
- Run Compose/UI tests when applicable.
- Manually test the affected flow on an emulator or physical device.

### Android branch examples

```text
feature/trip-list
feature/create-trip
fix/trip-details-navigation
refactor/trip-view-model
chore/update-gradle-dependencies
test/trip-use-case
```

### Android commit examples

```text
feat: add trip list screen
feat: add create trip view model
fix: correct trip details navigation
refactor: simplify trip use case
chore: update gradle dependencies
test: add trip view model tests
```

---

## Documentation

Update `README.md` or other documentation when a change affects:

- Installation.
- Project setup.
- Environment configuration.
- Architecture.
- API usage.
- User-visible behavior.
- Developer workflow.

---

## Definition of Done

A task is considered complete when:

- The requested behavior is implemented.
- The project builds successfully.
- Relevant tests pass.
- No known regression was introduced.
- Code follows the repository conventions.
- Secrets and local configuration are not committed.
- Documentation is updated when needed.
- The branch is pushed.
- A Pull Request is ready for review.

---

## Questions

If a requirement or architecture decision is unclear, discuss it before introducing a large structural change.

Keep changes focused, readable, and easy to review.
