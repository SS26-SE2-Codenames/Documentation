# Contributing to the Codenames Project

This document outlines the workflow and coding standards for our group project. 
Please follow these guidelines to ensure a smooth collaboration and high code quality.

## 1. Git Workflow
We follow a `Feature Branching` workflow.
- `main`: Always stable. Only contains finished, peer-reviewed milestones.
- `development`: The integration branch where all features are merged before going to main.
- `feature`: New functionality (e.g., `feature/game-logic`, `feature/socket-setup`).
- `misc`: (e.g., `fix/card-rendering`).

### Workflow Steps:
1. Take on a ticket.
2. Pull the latest changes from `develop`.
3. Create a new branch: `git switch -c feature/your-feature-name`.
4. Commit your changes using Conventional Commits (see below).
5. Ensure your branch is up to date with current codebase.
6. Push your branch and open a Pull Request (PR) to `development`.
7. Ensure PR only contains changes relevant to the ticket.
8. If multiple changes are to be made, a new branch should be created.

## 2. Commit Message Convention
To keep the history readable, use the following format:
`<type>(<scope>): <short summary>`

- `feature`: A new feature 
- `fix`: A bug fix
- `docs`: Documentation only changes
- `refactor`: Code changes that neither fix a bug nor add a feature
- There are other types of commits that can be made, but they have to be tagged accordingly.

## 3. Coding Standards
### General Rules
- **DRY Principle**: Do not repeat code. Extract or reuse if logic has already been implemented.
- **Language**: All code, comments, and documentation must be in English.
- **Google Code Style**: All PRs (Backend) must fulfill Google Code Style standards.
- **No rebase or squash merges**

### Documentation
- Java Docs as enforced by Google Code Style.

## 4. Pull Request & Peer Review
PRs must be made into `development` and not into `main`
1. **Self-Review**: Check your code for print statements or debug logs before submitting.
2. **Reviewer**: At least two other team members must approve the PR.
3. **Discussion**: Use PR comments to discuss architectural choices.

## 5. Testing
- 80% Code coverage as per SonarQube.
- Fix issues raised by SonarQube.
